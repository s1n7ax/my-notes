- First unlock the drive

```shell
udisksctl unlock -b /dev/sdc
```

- Then mount the drive as usual

```shell
udisksctl mount -b /dev/sdc1
```