---
slug: self-host-home-assistant-zigbee
title: 'Self-Host Home Assistant + Zigbee Smart Home (Full Tutorial)'
authors: s1n7ax
tags: [self-hosted, home-assistant, zigbee, docker, youtube]
description: Self-host Home Assistant with Docker and build a local Zigbee smart home - coordinator setup, stable device path, ZHA pairing, and your first device.
---

This is the companion post for the YouTube video. By the end you will have Home Assistant running in Docker on your own PC, with a Zigbee coordinator attached and your first Zigbee device paired and controllable — all local, no vendor cloud.

<!-- truncate -->

If you want the background first — WiFi vs Zigbee, which coordinator to buy, which devices to start with — read this first: [Intro to Smart Home](/Youtube/2025-11-02%20Intro%20to%20Smart%20Home).

## What you need

- A PC with Linux installed + Docker installed and running
  - Any old laptop, mini PC, or desktop with 4GB+ RAM works
  - Verify Docker: `docker --version && docker compose version`
- A Zigbee 3.0 USB coordinator (I use the SONOFF ZBDongle-P, Dongle-M/E also fine)
- At least one Zigbee device (smart plug is the best first device — easy + acts as a mesh router)
- A USB extension cable (highly recommended — keeps the coordinator away from USB 3.0 / SSD / PC case interference)

> [!WARNING]
> Plug the coordinator into a USB 2.0 port via an extension cable if you can. USB 3 noise on 2.4GHz is the #1 cause of "Zigbee is unstable" complaints.

## What we are building

```text
+-----------------+     Zigbee radio      +--------------------+    USB serial (/dev/serial/by-id/...)    +----------------------+      HTTP :8123      +-----+
| Zigbee device   | <-------------------> | USB Coordinator    | <---------------------------------------> | Home Assistant       | <------------------> | You |
| plug / sensor   |       2.4 GHz         | SONOFF ZBDongle-P  |            stable device path           | Docker container+ZHA |      browser       |     |
+-----------------+                       +--------------------+                                         +----------------------+                      +-----+
```

- **Home Assistant** is the brain (dashboards, automations)
- **ZHA** (Zigbee Home Automation) is the built-in Home Assistant integration that talks to the coordinator
- No MQTT, no Zigbee2MQTT, no cloud in this tutorial — simplest working stack

## Step 1 — Get the project

Repo: [`s1n7ax/youtube-home-assisatant-zigbee-tutorial`](https://github.com/s1n7ax/youtube-home-assisatant-zigbee-tutorial)

Clone it:

```bash
git clone https://github.com/s1n7ax/youtube-home-assisatant-zigbee-tutorial
cd youtube-home-assisatant-zigbee-tutorial
```

Or if you don't use git: open the repo page → **Code → Download ZIP** → extract it → `cd` into the extracted folder.

The project is just a `docker-compose.yml` that runs Home Assistant with the USB device passed through.

## Step 2 — Plug in the coordinator and find its stable path

1. Plug the Zigbee coordinator into a USB port (preferably via extension cable).
2. Find it:

```bash
ls -l /dev/serial/by-id/
```

Example output:

```bash
usb-Silicon_Labs_Sonoff_Zigbee_3.0_USB_Dongle_Plus_0001-if00-port0
```

3. The full stable path is:

```bash
/dev/serial/by-id/usb-Silicon_Labs_Sonoff_Zigbee_3.0_USB_Dongle_Plus_0001-if00-port0
```

> [!NOTE]
> Always use the `/dev/serial/by-id/...` path, not `/dev/ttyUSB0`. `ttyUSB0` can change to `ttyUSB1` on reboot or when you plug in another USB device. The `by-id` path is tied to the hardware and does not change.

If `ls /dev/serial/by-id/` is empty:

- Try another USB port / cable
- Run `dmesg | tail -20` right after plugging in to see if Linux detected it
- On some systems you need the `dialout` group: `sudo usermod -aG dialout $USER` then log out/in

## Step 3 — Set the device path in `docker-compose.yml`

Open `docker-compose.yml` in the project folder and replace the placeholder device path with your path from Step 2.

It looks something like this:

```yaml
services:
  homeassistant:
    # ...
    devices:
      - /dev/serial/by-id/usb-Silicon_Labs_Sonoff_Zigbee_3.0_USB_Dongle_Plus_0001-if00-port0:/dev/ttyUSB0
```

Left side = your real stable path on the host. Right side = path inside the container. Only change the left side.

Double-check with:

```bash
ls -l /dev/serial/by-id/usb-Silicon_Labs_Sonoff_Zigbee_3.0_USB_Dongle_Plus_0001-if00-port0
```

If that file doesn't exist, Home Assistant will fail to start — fix the path first.

## Step 4 — Start Home Assistant and open it

From the project folder:

```bash
docker compose up -d
docker compose ps
docker compose logs -f homeassistant
```

Then open in your browser:

```text
http://<your-pc-ip>:8123
```

- Running the browser on the same PC? Use `http://localhost:8123`
- From your phone (same WiFi)? Use the PC's LAN IP, e.g. `http://192.168.1.50:8123`

First boot takes a few minutes. Create your admin account when the onboarding wizard appears.

## Step 5 — Set up ZHA

1. In Home Assistant go to **Settings → Devices & Services → Add Integration**
2. Search for **Zigbee Home Automation (ZHA)**
3. When asked for the radio type / serial port, select your coordinator device (the `/dev/ttyUSB0` passed through, or the `by-id` path if shown)
4. Keep defaults for the rest and submit

If ZHA can't find the stick:

- Make sure the container actually has the device: `docker compose exec homeassistant ls -l /dev/ttyUSB0`
- Make sure no other program (Zigbee2MQTT, another ZHA instance) is using the same coordinator — one radio, one integration
- Restart the container after fixing the path: `docker compose restart`

## Step 6 — Pair your first Zigbee device and control it

1. Get your Zigbee device and put it into **pairing mode** following its manual. Usually one of:
   - Hold the button 5–10 seconds until the LED blinks
   - Power cycle it on/off 3–5 times
   - For a plug: hold the power button until it blinks rapidly
2. In Home Assistant go to **Settings → Devices & Services → ZHA → Add Device**
3. ZHA starts searching — the device should appear within 10–30 seconds. Keep it close to the coordinator for the first pairing.
4. Rename it to something useful (`Living Room Plug`, `Desk Lamp`, …).
5. Control it: click the device → toggle on/off. Add it to your dashboard with **Add to Dashboard**.

Suggested first test:

- Plug a lamp into the smart plug → toggle from Home Assistant → toggle from the physical button on the plug → confirm both states sync
- Then build one automation: **Settings → Automations → Create** (e.g. plug turns on at sunset)

## Troubleshooting

| Symptom | Fix |
| --- | --- |
| `by-id` empty | Different port/cable, check `dmesg`, extension cable away from USB 3 |
| HA starts but ZHA fails | Wrong device path, device busy, restart container |
| Device won't pair | Reset device to pairing mode again, bring it within 1–2m of coordinator, try again |
| Device drops off | Add a mains-powered Zigbee plug between coordinator and device — it acts as a router and strengthens the mesh |
| Can't open `:8123` | `docker compose ps` / `logs`, firewall, use LAN IP from phone |

## Next steps

- Add 2–3 Zigbee smart plugs early — every mains-powered device extends the mesh
- Then add battery devices: door sensor + motion sensor (classic first automation: door opens → light on)
- When simple automations get messy, move them to Node-RED or plain Home Assistant automations — your call
- Full background + device recommendations: [Intro to Smart Home](/Youtube/2025-11-02%20Intro%20to%20Smart%20Home)

Project repo for this video: [`s1n7ax/youtube-home-assisatant-zigbee-tutorial`](https://github.com/s1n7ax/youtube-home-assisatant-zigbee-tutorial)
