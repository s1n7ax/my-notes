# Bring OPI Back from Dead

- Install rkdeveloptool `nix shell nixpkgs#rkdeveloptool`
- Download SPL loader from [radxa](https://dl.radxa.com/rock5/sw/images/loader/rock-5b/release/)
- Download the latest firmware from [radxa](https://dl.radxa.com/rock5/sw/images/rock-5b/)

```
rkdeveloptool db rkxx_loader_vx.xx.bin
rkdeveloptool ul rkxx_loader_vx.xx.bin
```

- Install the OS to nvme or SD card
- Boot the OPI with the SD card or nvme
