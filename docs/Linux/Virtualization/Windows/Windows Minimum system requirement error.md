- Boot windows
- Hit `F10` to bring up the console
- Run `regedit`
- Go to `HKEY_LOCAL_MACHINE` > `SYSTEM` > `Setup`
- Create a new key in the `Setup` folder called `LabConfig`
- Create following `DWORD (32-bit) Value`s

```txt
BypassTPMCheck=1
BypassRAMChech=1
BypassSecureBootCheck=1
```

- Close the editor and hit Install Now