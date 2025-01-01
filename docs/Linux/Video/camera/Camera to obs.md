# Camera to OBS

- Install following

```bash
sudo apt install v4l2loopback-dkms gphoto2
```

- Start loopback device

```bash
sudo modprobe v4l2loopback exclusive_caps=1 max_buffer=2
```
- Stream camera feed to ffmpeg to video device

```bash
gphoto2 --stdout --set-config viewfinder=1 --capture-movie | ffmpeg -i - -vcodec copy -threads 1 -f v4l2 /dev/video0
```
