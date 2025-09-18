# Flashing Firmware and Changing IEEE on Sonoff ZBDongle-P

## Hardware Preparation

1. **Remove the cover** from the ZBDongle-P
2. **Enter bootloader mode**:
   - Press and hold the **boot button**
   - While holding boot, press the **reset button** for 2 seconds, then release it
   - Release the **boot button**

## Firmware Selection

1. Check the chipset compatibility guide: https://github.com/Koenkk/Z-Stack-firmware/blob/master/coordinator/README.md
2. For **CC2652P chipset**, download the `CC1352P2_CC2652P_launchpad_coordinator` zip file from: https://github.com/Koenkk/Z-Stack-firmware/releases
3. Extract the firmware zip file

## Flashing Tool Setup

1. Clone the flashing tool: https://github.com/JelmerT/cc2538-bsl
2. Extract the firmware files to the cc2538-bsl project directory
3. **For NixOS users**: Get required Python packages
   ```bash
   nix-shell -p "python3.withPackages (ps: with ps; [ pyserial intelhex ])"
   ```

## Flashing Process

Run the flashing command with your specific IEEE address:

```bash
sudo python cc2538_bsl/cc2538_bsl.py -p /dev/ttyUSB0 -evw CC1352P2_CC2652P_launchpad_coordinator_20250321.hex -i '0x00124b002e1dfa70'
```

### Command Parameters
- `-p /dev/ttyUSB0`: Serial port (adjust if needed)
- `-evw`: Erase, verify, and write
- `CC1352P2_CC2652P_launchpad_coordinator_20250321.hex`: Firmware file
- `-i '0x00124b002e1dfa70'`: Custom IEEE address

## Notes
- Make sure the device is in bootloader mode before flashing
- Replace the IEEE address with your desired value
- Verify the correct serial port with `dmesg` or `lsusb`