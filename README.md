# Al-Quran Subtitles
Al-Quran subtitles using FFMPEG

## Examples

### Example #1: Muxing the Audio & Video

```bash
    ffmpeg -y -i ./videos/input.mp4 \
    -i ./audios/Al-Fatihah.mp3 \
    -c copy -map 0:0 -map 1:0 ./videos/muxed.mp4
```

### Example #2: How to create a LightBox & DarkBox on the video

```bash
    ffmpeg -y -i ./videos/muxed.mp4 \
    -filter_complex \
    "drawbox=x=iw-w-10:y=ih-h-10:w=iw-20:h=150:t=fill:color=white@0.4" \
    -c:a copy ./output/lightbox.mp4
```

```bash
    ffmpeg -y -i ./videos/muxed.mp4 \
    -filter_complex \
    "drawbox=x=iw-w-10:y=ih-h-10:w=iw-20:h=150:t=fill:color=black@0.4" \
    -c:a copy ./output/darkbox.mp4
```

### Example #3: How to center the box position

```bash
    ffmpeg -y -i ./videos/input.mp4 \
    -filter_complex \
    "drawbox=x=iw-w-10:y=ih/2-h/2-10:w=iw-20:h=150:t=fill:color=black@0.4" \
    -c:a copy ./output/centerbox.mp4
```

### Example #4: How to burn the subtitles

```bash
    ffmpeg -y -i ./videos/muxed.mp4 \
    -filter_complex \
    "drawbox=x=iw-w-10:y=ih-h-10:w=iw-20:h=150:t=fill:color=black@0.4, \
    subtitles=./subtitles/al-fatihah.srt:fontsdir='./fonts':charenc='utf-8'" \
    -c:a copy ./output/subtitle.mp4
```

### Example #5: How to burn subtitles with the center box

```bash
    ffmpeg -y -i ./videos/muxed.mp4 \
    -filter_complex \
    "drawbox=x=iw-w-10:y=ih/2-h/2-10:w=iw-20:h=150:t=fill:color=black@0.4, \
    subtitles=./subtitles/al-fatihah.srt:fontsdir='./fonts':charenc='utf-8':force_style='shadowx=10,shadowcolor=Black,MarginV=100'" \
    -c:a copy ./output/subtitle.mp4
```

### Example #6: How to burn subtitles with the report

```bash
    FFREPORT=file=./logs/ffreport.log:level=32 \
    ffmpeg -y -i ./videos/muxed.mp4 \
    -filter_complex \
    "drawbox=x=iw-w-10:y=ih/2-h/2-10:w=iw-20:h=150:t=fill:color=black@0.4, \
    subtitles=./subtitles/al-fatihah.srt:fontsdir='./fonts':charenc='utf-8':force_style='shadowx=10,shadowcolor=Black,MarginV=100'" \
    -c:a copy ./output/subtitle.mp4
```

### Example #7: How to burn subtitles with the report ( with the current date & time )

```bash
    FFREPORT=file="./logs/$(date '+%d-%m-%y_%H-%M-%S').log":level=32 \
    ffmpeg -y -i ./videos/muxed.mp4 \
    -filter_complex \
    "drawbox=x=iw-w-10:y=ih/2-h/2-10:w=iw-20:h=150:t=fill:color=white@0.2, \
    subtitles=./subtitles/al-fatihah.srt:fontsdir='./fonts':charenc='utf-8':force_style='shadowx=10,shadowcolor=Black,MarginV=100'" \
    -c:a copy ./output/subtitle.mp4
```

### Example #7: How to burn subtitles into YouTube video size
Recommended resolution & aspect ratios
For the default 16:9 aspect ratio, encode at these resolutions:

 * 4320p (8k): 7680x4320
 * 2160p (4K): 3840x2160
 * 1440p (2k): 2560x1440
 * 1080p (HD): 1920x1080
 * 720p (HD): 1280x720
 * 480p (SD): 854x480
 * 360p (SD): 640x360
 * 240p (SD): 426x240

```bash
    ffmpeg -y -i ./videos/muxed.mp4 \
    -sub_charenc UTF-8 \
    -video_size 1280:720 \
    -filter_complex \
    "scale=1280:720,drawbox=x=iw-w-10:y=ih/2-h/2-10:w=iw-20:h=300:t=fill:color=white@0.2, \
    subtitles=./subtitles/al-fatihah.srt:fontsdir='./fonts':force_style='shadowx=10,shadowcolor=Black,MarginV=100'" \
    -c:a copy ./output/subtitle.mp4
```

## Remember:

> [!NOTE]
> This is an open source project and free.

> [!IMPORTANT]
> Share our repository.