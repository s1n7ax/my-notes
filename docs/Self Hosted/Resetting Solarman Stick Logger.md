# Resetting Solarman Stick Logger

According to the official Solarman document *"Stick Logger Quick Guide USER MANUAL for SOLARMAN"*, the proper way to reset the logger is:

1. Press and hold the **reset button for 10 seconds**.
2. After 4 seconds, all lights will be extinguished.
3. The **READY** light will start flashing fast (every 100ms).

## When the official reset does not work

Sometimes the reset process above does not work. The trick that has worked reliably:

1. Turn off the Wi-Fi device (router/AP) the logger is currently connected to.
2. Wait for about **10 minutes**.
3. The logger will fall back into AP mode and the `AP_xxxxxxxx` Wi-Fi network will appear.
4. Connect to that `AP_xxx` Wi-Fi network.
5. Open a browser and go to `http://10.10.100.254` to access the logger's gateway/configuration page.

## Tips

- Once connected to the home network, assign the logger a **static IP** from the router's DHCP reservations. This makes integration with **Home Assistant** stable, since the integration relies on the logger's IP staying the same.
