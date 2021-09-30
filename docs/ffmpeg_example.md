# Ffmpeg example commands


#### Basic Transcoding Examples
```
ffmpeg -i input.mov -c:v libx264 -c:a mp2 -vb 1000000 -ab 128k output.ts

ffmpeg -i input.mov -c:v libx264 -x264opts keyint=25:min-keyint=25:scenecut=-1 -acodec libfdk_aac -streamid 0:2064 -streamid 0:2068 -g 25 -vb 1800k -ab 128k output.ts
```


#### Image to Video

```
ffmpeg -i input.png -r 25 -t 30 -vcodec h264 -an  video.mov
```

#### Extract Specific Frame as Image

```
ffmpeg -ss 55 -i IH_PA_NJSPINDOTD_01.ts -t 0.040 -f image2 colorbar2.jpg
```

#### Text Overlay

Command to scale input video to 320x256 add frame number on the bottom right corner

```
ffmpeg -i IH_PA_SCDKNGHTME_02.ts -ss 184.960 -s 320x256 60 -vf "drawtext=fontsize=24:fontfile=/usr/share/fonts/truetype/freefont/FreeMono.ttf: text=%{n}: x=w-tw: y=h-lh: fontcolor=white" -acodec copy o.mov
```