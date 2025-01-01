Davinci resolve free version cannot import h264 mp4 files. So as a workaround,
you can convert the file into a mjpeg and import. To convert all the files the
mp4 files in the current directory into mjpeg use the following ffmpeg script

```sh
mkdir transcoded; for i in *.mp4; do ffmpeg -i "$i" -vcodec mjpeg -q:v 2 -acodec pcm_s16be -q:a 0 -f mov "transcoded/${i%.*}.mov"; done
```
