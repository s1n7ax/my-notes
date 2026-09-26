# Intro to Smart Home

---

## What we are actually building

- A light/plug/sensor you can control **without** the vendor's cloud
- Stuff that keeps working when the internet is down
- Automations - "if motion and it's dark, turn on the light"

> [!NOTE]
> Buying a smart bulb is not a smart home. Owning the brain is.

---

## Cheapest way to get started

### Prerequisites

> [!NOTE]
> WiFi network should be 2.4GHz not 5GHz

- Buy WiFi device
- Install the (what ever they say we should use) app on mobile
- Follow the instructions in manual to connect the device

> [!WARNING]
> I don't use these apps nor trust them
>
> - Device talks to a server in another country to turn on a bulb 2 meters away
> - Vendor can kill the app/cloud any day and your hardware becomes e-waste
> - It's fine to start here. Just don't build the whole house on it

---

### Where to buy devices

- [Daraz](https://www.daraz.lk)
- [Temu](https://www.temu.com/)
- [Ali express](https://www.aliexpress.com/)

---

### How to find devices

- Search by brand
  - Tuya (cheap)
  - Moes (mid)
  - Sonoff (mid/expensive)
  - Aqara (expensive)

- Search by device type
  - WiFi/Smart bulb
  - WiFi/Smart switch
  - WiFi/Smart plug

### Brands - what I learned the hard way

> [!WARNING] Tuya
>
> - LED Bulbs get pretty hot, and some of them stopped working after few months
> - Plug stops working completely or relay stops working after few months
> - "Tuya" is not really a brand - it's a platform. Same white box, 50 different seller names

> [!WARNING] Moes
>
> - They lie sometimes - Human presence sensor is not a presence sensor

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

## Zigbee Coordinator

A Zigbee coordinator is a device that acts as a hub for your Zigbee network.

### Types of Zigbee Coordinators

> [!NOTE]
>
> - There are different versions of Zigbee coordinators. Buy the 3.0 version (latest)

- Which coordinator to buy?
  - No PC?
    - Tuya ZigBee 3.0 Multimode Gateway - cheapest, but cloud
  - Got PC?
    - **SONOFF Dongle-M (dual antenna)** - This is the one I recommend
    - SLZB-06 - Ethernet/PoE, only if the server is a bad spot for a radio. It did not work for me - see below

> [!WARNING]
> Keep the coordinator away from the USB 3.0 ports / SSD / the PC case. USB 3 noise kills 2.4GHz.
> Use a USB extension cable - this fixes most "Zigbee is unstable" complaints

---

#### Tuya ZigBee 3.0 Multimode Gateway

![tuya gateway top](../../assets/2025-11-02-14-15-55.jpg)

- Cheapest way in, no PC needed
- But it's a **cloud** gateway - back to the vendor app
- Buy this only if you are not going to run Home Assistant

---

#### Tuya gateway - ports and pairing button

![tuya gateway side - USB-C power and pairing button](../../assets/2025-11-02-14-16-02.jpg)

---

#### Tuya gateway - product shot

![tuya](../../assets/2025-11-02-14-15-41.png)

---

#### SONOFF USB dongles

![sonoff plugged into the server](../../assets/2025-11-02-14-16-45.jpeg)

- **ZBDongle-P** (TI CC2652P) - the safe, boring, well supported one
- **ZBDongle-E** (Silabs EFR32MG21) - newer, was rough on firmware early on
- Plugs into the PC/server running the software

---

#### SONOFF USB dongles - product shot

![sonoff](../../assets/2025-11-02-14-16-23.png)

---

### SONOFF Dongle-M (Recommend)

![sonoff dongle-m](../../assets/2025-11-02-14-16-33.png)

---

#### SLZB-06

![slzb with external antenna](../../assets/2025-11-02-14-17-20.jpg)

- Ethernet / PoE / WiFi / USB - put it in the middle of the house, not next to the server
- On paper the best placement of the three

> [!WARNING]
> This did not work for me - devices kept dropping off the network
> ([this issue](https://github.com/Koenkk/zigbee2mqtt/issues/17809)). I switched to the SONOFF Dongle-M

---

#### SLZB-06 - product shot

![slzb](../../assets/2025-11-02-14-17-03.png)

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

- Cameras, lights, AC, water tank - all in one place, no vendor apps
- Works on the phone the same way it works on the browser

---

### My Home Assistant dashboard

![home assistant dashboard - AC and lights](../../assets/2026-09-22-ha-dashboard-2.png)

---

### Node-RED

[Node-RED](https://nodered.org/) - drag and drop automations. Install it as a Home Assistant add-on

- Home Assistant automations are fine for "if this then that"
- Node-RED is for the messy ones - loops, delays, retries, branching you can actually see on screen
- Both can run at the same time. Same devices, different editor

> [!NOTE]
> Not required. Start with Home Assistant automations and only move the ugly ones to Node-RED

---

#### Home Assistant automation

![home assistant automation editor - turn off water pump on overflow](../../assets/2026-09-22-ha-automation.png)

- When / And if / Then do - one trigger, one action, done in a minute
- Perfect for "flood sensor is wet -> kill the pump"

---

#### Node-RED flow

![node-red flow - bathroom lights](../../assets/2026-09-22-node-red-flow.png)

- Same idea, but you can see the whole thing - waits, branches, timers
- This one is just "bathroom lights": door opened, is anyone inside, wait for motion, wait for
  door to close, keep lights on 5 minutes
- Try writing that as a single Home Assistant automation and you will understand why Node-RED exists

---

## Devices to buy

### Door / window contact sensor

![zigbee door contact sensor - magnet and body](../../assets/2026-09-22-door-sensor.jpg)

- Two parts - body on the frame, magnet on the door. Open/closed, that's it
- Battery powered, so Zigbee. Lasts a year or more
- The one automation everyone builds first - door opens, light comes on

---

### Motion sensor (SONOFF PIR)

![sonoff zigbee PIR motion sensor in hand](../../assets/2026-09-22-sonoff-motion-sensor.jpg)

- PIR - detects **movement**, not presence. Sit still and it thinks the room is empty
- Magnetic base, stick it in a corner
- Pair it with the door sensor so lights stay on while you are actually in the room

> [!WARNING]
> If you want "someone is in the room doing nothing", you need an mmWave presence sensor,
> not a PIR. And Moes lies about which one they are selling

---

### Smart plug (Zigbee 3.0)

![zigbee smart plug - back, model and ratings](../../assets/2026-09-22-zigbee-plug-back.jpg)

![zigbee smart plug - front socket](../../assets/2026-09-22-zigbee-plug-front.jpg)

- Easiest win - plug it in, no wiring, nothing to switch off at the breaker
- Most of them report power usage, so you know what your fridge/pump actually costs
- **Mains powered = Zigbee router**. Buy 2-3 early and your mesh gets stronger for free
- Check the rated current before you put a water pump or a heater on it (this one is 20A)

---

### In-wall relay module (SONOFF MINI)

![sonoff mini relay module - N, L Out, L In, S1, S2 terminals](../../assets/2026-09-22-sonoff-mini-relay.jpg)

- Goes **behind** the existing wall switch, inside the back box
- The physical switch keeps working (S1/S2) and Home Assistant can also control it
- Best option when you want the room to look normal and still be automated
- Needs neutral (N) at the switch box - a lot of older houses do not have it

> [!WARNING]
> Mains voltage. If you are not comfortable inside a switch box, get an electrician

---

### Smoke detector (Aqara)

![aqara zigbee smoke detector](../../assets/2026-09-22-aqara-smoke-detector.jpg)

- Screams locally **and** pushes a notification to your phone
- This is the one where local control actually matters - it must work when the internet is down
- Test button on the front, replace it when the firmware says the sensor is end of life

---

## My suggested starting kit

1. Zigbee coordinator (SONOFF Dongle-M, dual antenna)
2. Home Assistant on anything with 4GB RAM
3. 2-3 Zigbee smart plugs - they are also mesh routers
4. 1 motion sensor + 1 door sensor
5. Build one automation you actually use, then grow
