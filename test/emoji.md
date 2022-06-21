---
sort: 5
---

# GStreamer

## Preinstallation

```console
$ sudo apt-get install v4l-utils
```

**Check v4l devices**
```console
$ v4l2-ctl --list-devices
```

**Check supported format**
```console
$ v4l2-ctl -d /dev/video0 --list-formats-ext
```

**Check connected devices**
```console
$ v4l2-ctl --list-formats-ext
```

## Commands

**Hello World**
```console
$ gst-launch-1.0 videotestsrc ! 'video/x-raw, width=(int)1280, height=(int)720, format=(string)I420, framerate=(fraction)30/1' ! nveglglessink -e
```

### vl4 device

Simple display
```console
$  gst-launch-1.0 v4l2src ! xvimagesink
```
or
```console
$ gst-launch-1.0 -ev v4l2src device=/dev/video1 ! xvimagesink
```

### Save As .mp4

Using h264 codec:
```console
$ gst-launch-1.0 videotestsrc ! 'video/x-raw, width=(int)1280, height=(int)720, format=(string)I420, framerate=(fraction)30/1' ! omxh264enc ! 'video/x-h264, stream-format=(string)byte-stream' ! h264parse ! qtmux ! filesink location=test.mp4 -e

```

### Read video file

Read `.mp4` and decodeing:
```console
$ gst-launch-1.0 filesrc location=test.mp4 ! qtdemux name=demux ! h264parse ! omxh264dec ! nveglglessink -e
```

### Read webcam and encoding stream
```console
$ gst-launch-1.0 v4l2src device=/dev/video1 ! decodebin ! videoconvert ! omxh264enc ! h264parse ! omxh264dec ! nveglglessink -e
```

### RTP Streaming

Send to host port 5000:
```console
$ gst-launch-1.0 v4l2src device=/dev/video1 ! decodebin ! videoconvert ! omxh264enc ! video/x-h264, stream-format=byte-stream ! rtph264pay ! udpsink host=127.0.0.1 port=5000
```

Receive Streaming:
```console
$ gst-launch-1.0 udpsrc port=5000 ! application/x-rtp, encoding-name=H264, payload=96 ! rtph264depay ! h264parse ! omxh264dec ! nveglglessink -e
```

### Jpg image processing

```bash
gst-launch-1.0 multifilesrc location=img_%06d.jpg caps=image/jpeg,framerate=30/1 ! jpegdec ! videoconvert ! jpegenc ! multifilesink location=jpgs/img_post_%06d.jpg
```


