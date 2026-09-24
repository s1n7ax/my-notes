# Intro to Smart Home

---

## What we are actually building

- A light/plug/sensor you can control **without** the vendor's cloud
- Stuff that keeps working when the internet is down
- Automations - "if motion and it's dark, turn on the light"

> [!NOTE]
> Buying a smart bulb is not a smart home. Owning the brain is.

---

## WiFi vs Zigbee

For a smart-home network, both Wi-Fi and Zigbee work well - but they shine in very different roles

|                 | WiFi                 | Zigbee                               |
| --------------- | -------------------- | ------------------------------------ |
| Extra hardware  | None                 | Coordinator needed                   |
| Power draw      | High                 | Very low                             |
| Battery devices | Bad idea             | Made for it                          |
| Range           | Router's range       | Mesh - every mains device extends it |
| Device count    | Router starts crying | Hundreds                             |
| Bandwidth       | High (camera/audio)  | Tiny (on/off, sensor values)         |

### Recommendation

Use both

- **Zigbee** - everything battery powered (sensors, buttons, door contacts) and wall switches
- **WiFi** - cameras, speakers, anything that moves real data

> [!NOTE]
>
> - Zigbee also uses 2.4 GHz so to reduce interference by selecting channels that are not used by WiFi
> - WiFi 1 / 6 / 11 -> pick Zigbee 15, 20, 25 or 26
> - Every **mains powered** Zigbee device is a router and makes the mesh stronger. Battery devices never repeat

> [!TIP]
> Before buying anything, search the model name on
> [Zigbee2MQTT supported devices](https://www.zigbee2mqtt.io/supported-devices/) and
> [Blakadder](https://zigbee.blakadder.com/). If it's not there, you may be on your own

---

## Getting started: Budget to Capable

### Tier 1: Cheapest local setup (~$20-50)

SONOFF Dongle-P on any old PC/laptop you have lying around.

#### SONOFF USB dongles

![sonoff plugged into the server](../../assets/2025-11-02-14-16-45.jpeg)

- **ZBDongle-P** (TI CC2652P) - **Start here** - boring, rock solid, cheap
- **ZBDongle-E** (Silabs EFR32MG21) - newer option, also works
- Plugs into the PC/server running Home Assistant

![sonoff](../../assets/2025-11-02-14-16-23.png)

---

### Tier 2: Better antenna setup (~$80-150)

SONOFF Dongle-M with better range and dual antenna. Same coordinator principle, better performance.

#### SONOFF Dongle-M (Recommended upgrade)

![sonoff dongle-m](../../assets/2025-11-02-14-16-33.png)

- Dual antenna - less dead zones
- Same PC/server setup as Tier 1, just plug it in
- Worth the upgrade if you're expanding beyond 2-3 rooms
- Keep away from USB 3.0 ports / SSD / PC case - USB 3 noise kills 2.4GHz. Use USB extension cable.

---

### Tier 3: Dedicated hub placement (~$200+)

SLZB-06 - Ethernet/PoE, lets you place the radio in the center of your house instead of next to the server.

#### SLZB-06

![slzb with external antenna](../../assets/2025-11-02-14-17-20.jpg)

![slzb](../../assets/2025-11-02-14-17-03.png)

- Ethernet / PoE / WiFi / USB - put it in the middle of the house, not next to the server
- On paper, best signal coverage of all three
- This did not work for me - devices kept dropping off the network. I switched to Dongle-M instead.

---

### What not to do: Cloud gateways

#### Tuya ZigBee 3.0 Multimode Gateway

![tuya gateway top](../../assets/2025-11-02-14-15-55.jpg)

![tuya gateway side - USB-C power and pairing button](../../assets/2025-11-02-14-16-02.jpg)

![tuya](../../assets/2025-11-02-14-15-41.png)

- Cheapest hardware price, no PC needed
- **But it's a cloud gateway** - device data goes to Tuya's servers to turn on a light 2 meters away
- Vendor can kill it any day, hardware becomes e-waste
- Skip this. Even the Tier 1 option is better for long-term ownership

---

## The brain

A coordinator is just a radio. Something has to run the logic

- [Home Assistant](https://www.home-assistant.io/) - the one I use. Runs on a mini PC, an old laptop, a Pi
- Zigbee integration options:
  - **Zigbee2MQTT** - widest device support, more control
  - **ZHA** - built into Home Assistant, less setup

> [!NOTE]
> Pick one. Running both on the same dongle is not a thing

---

### My Home Assistant dashboard

![home assistant dashboard - cameras and quick access](../../assets/2026-09-22-ha-dashboard-1.png)

![home assistant dashboard - AC and lights](../../assets/2026-09-22-ha-dashboard-2.png)

- Cameras, lights, AC, water tank - all in one place, no vendor apps
- Works on the phone the same way it works on the browser

---

### Node-RED (when you need complexity)

[Node-RED](https://nodered.org/) - drag and drop automations. Install it as a Home Assistant add-on

- Home Assistant automations are fine for "if this then that"
- Node-RED is for the messy ones - loops, delays, retries, branching you can actually see on screen
- Not required. Start with Home Assistant automations and only move the ugly ones to Node-RED

#### Home Assistant automation

![home assistant automation editor - turn off water pump on overflow](../../assets/2026-09-22-ha-automation.png)

- When / And if / Then do - one trigger, one action, done in a minute
- Perfect for simple: "flood sensor is wet → kill the pump"

#### Node-RED flow

![node-red flow - bathroom lights](../../assets/2026-09-22-node-red-flow.png)

- Same idea, but you can see the whole thing - waits, branches, timers
- "Bathroom lights": door opened → anyone inside? → wait motion → wait door close → lights on 5 min
- Try that as Home Assistant automation and you'll understand why Node-RED exists

---

## Where to buy and what brands to trust

### Where to buy devices

- [Daraz](https://www.daraz.lk)
- [Temu](https://www.temu.com/)
- [Ali express](https://www.aliexpress.com/)

### Device brands by price and reliability

- **Tuya** (cheap) - White-box platform, not a real brand. Bulbs run hot, plugs fail within months
- **Moes** (mid) - Decent price, but they mislabel sensors (presence vs. motion)
- **Sonoff** (mid/expensive) - Reliable, well-supported in Zigbee2MQTT
- **Aqara** (expensive) - Solid devices, high quality, best if budget allows

### How to find devices

Search by device type, match it to supported coordinators:

- **Zigbee devices** (battery powered, sensors, wall switches, plugs)
  - Search Zigbee2MQTT supported list FIRST before buying
  - [Zigbee2MQTT supported devices](https://www.zigbee2mqtt.io/supported-devices/)
  - [Blakadder device database](https://zigbee.blakadder.com/)

- **WiFi devices** (cameras, speakers, anything that streams data)
  - Use WiFi for high-bandwidth only
  - Most WiFi devices still work locally; check before buying

> [!NOTE]
> Before buying anything, search the model name on Zigbee2MQTT. If it's not there, you may be on your own

---

## Devices to buy: Tier your setup

Start with **Tier 1**, add **Tier 2** after you have the brain working, go **Tier 3+** as you grow.

### Tier 1: First automation (~$5-20 each)

#### Door / window contact sensor

![zigbee door contact sensor - magnet and body](../../assets/2026-09-22-door-sensor.jpg)

- Two parts - body on the frame, magnet on the door. Open/closed, that's it
- Battery powered, so Zigbee. Lasts a year or more
- Build your first automation: "door opens → light comes on"

#### Smart plug (Zigbee 3.0)

![zigbee smart plug - back, model and ratings](../../assets/2026-09-22-zigbee-plug-back.jpg)

![zigbee smart plug - front socket](../../assets/2026-09-22-zigbee-plug-front.jpg)

- Plug it in, no wiring, nothing to switch off at breaker
- Reports power usage - know what your devices actually cost
- **Mains powered = Zigbee router**. Buy 2-3 to strengthen the mesh
- Check rated current before heavy loads (this one is 20A)

---

### Tier 2: Smarter automations (~$10-30 each)

#### Motion sensor (SONOFF PIR)

![sonoff zigbee PIR motion sensor in hand](../../assets/2026-09-22-sonoff-motion-sensor.jpg)

- PIR detects **movement**, not presence. Sit still = room looks empty
- Pair with door sensor: "door opens AND motion → light on"
- Magnetic base - stick in corner
- For true presence (idle detection), you need mmWave sensor, not PIR

---

### Tier 3: Wired control (~$50-150 + electrician)

#### In-wall relay module (SONOFF MINI)

![sonoff mini relay module - N, L Out, L In, S1, S2 terminals](../../assets/2026-09-22-sonoff-mini-relay.jpg)

- Goes **behind** the existing wall switch, inside the back box
- Physical switch keeps working, Home Assistant can also control it
- Room looks normal but fully automated
- Needs neutral (N) at switch box - many older houses don't have it
- **Mains voltage** - get electrician if not comfortable

---

### Tier 4: Safety-critical (~$50+)

#### Smoke detector (Aqara)

![aqara zigbee smoke detector](../../assets/2026-09-22-aqara-smoke-detector.jpg)

- Screams locally **and** notifies your phone
- Works when internet is down - this device **must** work offline
- Test button on front, replace when firmware says sensor is end-of-life

---

## Getting started: Month-by-month plan

**Month 1: Build the foundation**
- SONOFF Dongle-P (or old USB receiver you have)
- Home Assistant on any PC with 4GB RAM (old laptop counts)
- 1-2 door sensors
- 1 smart plug
- **Goal:** One working automation (door opens → light/plug turns on)

**Month 2: Expand the mesh**
- Upgrade to SONOFF Dongle-M if the range sucks
- Add 2-3 more smart plugs (mesh routers strengthen the network free)
- Add 1 motion sensor
- **Goal:** "Door opens + motion → light on 10 minutes, then off"

**Month 3: Real automations**
- Add devices for rooms you actually use
- Move complex automations to Node-RED
- Build the dashboard so you actually use it
- **Goal:** 3-4 automations that save you time daily

**Later: As budget allows**
- In-wall relays (needs electrician, but looks normal)
- Presence sensors (mmWave, if you need idle detection)
- Cameras (on WiFi)
- Dedicated server for reliability
