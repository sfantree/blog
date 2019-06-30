---
title: Maruko's Toolbox（小丸工具箱）命令行版本移植 
date: 2019-06-30 08:59:35
tags: [FFmpeg]
categories: 技术控 
---

小丸工具箱是一款个人开发的压制工具，作者将常用转码工具进行打包，使用户可以充分利用x264编码的优越性，在保证画质清晰的同时减小视频体积，发布版本为跨平台的GUI版本，但个人需求为充分利用多核云主机的运算性能，受制于平台限制，只能在命令行下进行操作。于是我简单分析了下压制日志的各种命令，改写了简化部分操作的命令行版本。

```bash
#!/bin/bash
echo "recode audio stream from $1"
ffmpeg -i $1 -vn -sn -c:a aac -map 0:a:0 $1.aac
echo "recode video stream from $1"
ffmpeg -i $1 -an -c:v libx264 -x264-params crf=23.5:ref=4:bframes=3:keyint=250:min-keyint=1:scenecut=60:deblock=1,1:qcomp=0.5:psy-rd=0.3,0:aq-mode=2:aq-strength=0.8 $1.mp4
#ffmpeg -i $1 -an -c:v libx264 -x264-params crf=23.5:ref=4:bframes=3:keyint=250:me=umh:min-keyint=1:scenecut=60: \
            deblock=1,1:qcomp=0.5:psy-rd=0.3,0:aq-mode=2:aq-strength=0.8 $1.mp4
echo "merge audio stream and video stream to $1_x264.mp4"
ffmpeg -i $1.mp4 -i $1.aac  -map 0:0 -map 1:0 -shortest $1_x264.mp4
#echo "remove $1.mp4 $1.aac"
#rm $1.mp4 $1.aac
```

直接使用默认配置的参数，替换了原来的x264二进制文件为FFmpeg，静态编译的FFmpeg二进制文件下载地址 [FFmpeg Static Builds](https://johnvansickle.com/ffmpeg/)


