# Flashing custom rom

- Reboot to bootloader `adb reboot bootloader`
- Flash the recovery `fastboot flash recovery <path to recovery file>`
- Reboot to the recovery `fastboot reboot recovery`
- Go to advanced *Wipe* and *Advanced Wipe*
- Clean the following
    - Dalvik / ART Cache
    - Data
    - Cache
- Go to *Install*
    - Select Firmware
    - Tap *Add more Zips*
    - Select Custom ROM
    - Tap *Add more Zips*
    - Select Magisk
- Swipe *Swipe to confirm Flash*
- Go to *Home* -> *Wipe* -> *Format Data*
- Type *Yes* and continue
- Tap *Reboot System*

