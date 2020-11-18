# Awesome FFMPEG

Useful commands for FFMPEG used to convert video and audio files.

## Summary

- [Links](#links)
- [Video commands](#video-commands)
- [Audio commands](#audio-commands)
- [Miscellaneous](#miscellaneous)
- [Codec guides](#codec-guides)
- [Blog posts](#blog-posts)

⚠️ In this document, user vars will be marked with a `$`. `$FILE` for your input or output file, `$INPUT` for your input file, `$OUTPUT` for your output file, etc

## Links

[⬆️ Go to top](#summary)

- [Official website](https://ffmpeg.org/)
- [FFMPEG in the browser](https://github.com/ffmpegwasm/ffmpeg.wasm)

**Installation**
- [Installation with homebrew for MacOS](https://github.com/homebrew-ffmpeg/homebrew-ffmpeg/)

**Integration**
- [youtube-dl](https://github.com/ytdl-org/youtube-dl)

**Packages**
- [Package for node.js](https://github.com/xonecas/ffmpeg-node)
- [Package for PHP](https://github.com/PHP-FFMpeg/PHP-FFMpeg)
- [Package for Laravel](https://github.com/protonemedia/laravel-ffmpeg)

## Video commands

[⬆️ Go to top](#summary)

### Convert video for the web

Where `$WITH` is the desired video width. 

**VP9 (.webm)**

`ffmpeg -i $INPUT -vcodec libvpx -acodec libvorbis -ac 2 -b:a 96k -ar 44100 -vf scale=$WIDTH:-1 -map 0 $OUTPUT.webm`

**H264 (.mp4)**

`ffmpeg -i $INPUT -vcodec libx264 -acodec libfdk_aac -ac 2 -ar 48000 -b:a 96k -vf scale=$WIDTH:-1 -map 0 $OUTPUT.mp4`

**Vorbis (.ogv)**

`ffmpeg -i $INPUT -vcodec libtheora -acodec libvorbis -b:a 96k -vf scale=$WIDTH:-1 -map 0 $OUTPUT.ogv`

### Video to GIF

`ffmpeg -i $INPUT $OUTPUT.gif`

### Cut a video without re-encoding (fast)

Where `$START` and `$END` are the timecodes in format `HH:MM:SS`.

```bash
ffmpeg -i $INPUT -ss $START -to $END -c copy $OUTPUT
# Ex: ffmpeg -i video.mp4 -ss 00:00:00 -to 00:01:30 -c copy cut.mp4
```

### Extract images from a video every X seconds

Where `$RATE` is desired images per second: `0.5` for 1 image every 2 seconds, `0.1` for 1 image every 10 seconds, etc).

```bash
ffmepg -i $INPUT -r $RATE -f image2 $OUTPUT_%05d.jpg
# Ex: ffmepg -i awesome_goal.mp4 -r 0.1 -f image2 goal_%05d.jpg
```

### Loop a video into a longest one

Where `$ITERATION` is the desired video loops.

`ffmpeg -stream_loop $ITERATION -i $INPUT -c copy $OUTPUT`

## Audio commands

[⬆️ Go to top](#summary)

### Extract audio from a video in MP3

Where `$BITRATE` is the desired audio bitrate (96, 128, 192, 256, 320).

```bash
ffmpeg -i $INPUT -vn -ar 44100 -ac 2 -ab $BITRATE -f mp3 $OUTPUT.mp3
# Ex: ffmpeg -i i_love_rock_n_roll.mp4 -vn -ar 44100 -ac 2 -ab 192 -f mp3 i_love_rock_n_roll.mp3
```

## Miscellaneous

[⬆️ Go to top](#summary)

### Get file infos

`ffmpeg -i $FILE`

### Get file infos in JSON format

`ffprobe -loglevel quiet -show_format -show_streams -print_format json $FILE`

## Codec guides

[⬆️ Go to top](#summary)

**Video**
- [h264](https://trac.ffmpeg.org/wiki/Encode/H.264)
- [h265 (HEVC)](https://trac.ffmpeg.org/wiki/Encode/H.265)

**Audio**
- [mp3](https://trac.ffmpeg.org/wiki/Encode/MP3)
- [aac](https://trac.ffmpeg.org/wiki/Encode/AAC)

## Blog posts

[⬆️ Go to top](#summary)

- [A Large-Scale Comparison of x264, x265, and libvpx — a Sneak Peek](https://netflixtechblog.com/a-large-scale-comparison-of-x264-x265-and-libvpx-a-sneak-peek-2e81e88f8b0f?gi=51b962fb1116) from [The Netflix Tech Blog](https://netflixtechblog.com/)