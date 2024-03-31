---
title: ffmpeg 一个跨平台的开源免费的媒体文件处理工具
tags: [computer]
---


## 用法
ffmpeg是命令行工具,通过官网下载链接解压缩得到ffmpeg文件,通过shell窗口运行

```
ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfile}...
```

-i 选择输入的文件(可以是视频文件,也可以是网络流等),每个文件可以包含多个不同类型的流,流的类型可用缩写(v视频、a音频、s字幕、d数据、t附件)  
要引用输入文件内容,必须使用他们的索引(从0开始).比如`1:a`指第2个文件的所有音频文件,`2:3`是指第3个文件的第4个流.

### Stream selection 流的选择
有如下三个文件
```
input file 'A.avi'
      stream 0: video 640x360
      stream 1: audio 2 channels

input file 'B.mp4'
      stream 0: video 1920x1080
      stream 1: audio 2 channels
      stream 2: subtitles (text)
      stream 3: audio 5.1 channels
      stream 4: subtitles (text)

input file 'C.mkv'
      stream 0: video 1280x720
      stream 1: audio 2 channels
      stream 2: subtitles (image)
```

`ffmpeg -i A.avi -i B.mp4 out1.mkv out2.wav -map 1:a -c:a copy out3.mov`  
共输出3个文件:  
- out1.mkv文件,ffmpeg会自动选择最优的音视频流,也就是B.mp4中的stream 0和stream 3,字幕则会选择最早出现的B.mp4中的stream 2.  
- out2.wav文件,因为wav时音频文件,所以选择B.mp4中的stream 3.  
- out3.mov文件,`-map 1:a`第二个文件也就是B.mp4的所有音频文件,`-c:a copy`音频不转码.

`ffmpeg -i C.mkv out1.mkv -c:s dvdsub -an out2.mkv`  
共输出2个文件:
- out1.mkv文件,由于C.mkv中的字幕是基于图像的,而mkv封装格式默认的字幕格式是基于文字的,所以字幕流将被丢弃.
- out2.mkv文件,`-c:s dvdsub`字幕的编码为dvdsub,所以字幕将被封装进文件中,`-an`表示不要音频.

`ffmpeg -i A.avi -i C.mkv -i B.mp4 -filter_complex "overlay" out1.mp4 out2.srt`  
共输出两个文件:
- out1.mp4文件,`-filter_complex "overlay"`这个参数需要两个视频文流,由于没有指定,所以选择前两个也就是A.avi和C.mkv中的视频流进行叠加
- out2.srt文件,因为字幕只支持基于文字的字幕,而C.mkv中的是基于图像的,所以选择了B.mp4中的stream 2字幕流.

### options 参数

`-c[:stream_specifier] codec (input/output,per-stream)`
`-c`和`-codec`一样,用来定义每一条流使用的编解码器


## Tips 提示
Apple's _H_._265_ codec _tag_ is hvc1 while Handbrake currently generates hev1. Quicktime on macOS High Sierra cannot play hev1 _H_._265_ files.
输出视频到macos端观看的话选择code_tag为hvc1


## Reference 参考：
[ffmpeg官方文档](http://ffmpeg.org/ffmpeg-all.html)

  
  


