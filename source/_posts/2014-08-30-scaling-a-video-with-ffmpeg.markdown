---
layout: post
title: "Scaling a video with FFmpeg"
date: 2014-08-30 16:06
comments: true
categories: 
---

When I started out at Movideo, our platform only supports 16:9 and 4:3 videos. As Movideo grows, I realized that the bigger studios doesn't necessarily deals with 16:9 and 4:3 anymore. Obviously, resizing a mezzanine video with the `-s` command doesn't work anymore because you might end up with stretchy videos.

A few weeks back I've been tasked to make some changes so that FFmpeg will scale the video based on height. For example, if a video is 640x360, and the given height to encode is 720, the output video should be 1280x720.

After doing some research, I found a <a href="http://stackoverflow.com/questions/8218363/maintaining-ffmpeg-aspect-ratio">StackOverflow post</a> with the solution. The answer was to use FFmpeg's video filter `-vf scale=-1:360`. That only works when the scaled width is an even number. If the scaled width is an odd number, you'll get the following error `height not divisible by 2`.

The same post also states that to scale the height based on the width, you'll need to do `scale=640:trunc(ow/a/2)*2` to prevent the `height not divisible by 2` error. So if you need to scale by height, the command would be 

`-vf scale=trunc(oh*a/2)*2:720`

Unfortunately, we're also using FFmpeg to do watermarking on videos and you cannot have 2 video filter command in FFmpeg. Luckily, you can merge both the video filter command into one video filter command by doing the following:

`-vf "movie=watermark.png [watermark]; [in][watermark] overlay=10:main_h-overlay_h-10 scale=trunc(oh*a/2)*2:720 [out]"`