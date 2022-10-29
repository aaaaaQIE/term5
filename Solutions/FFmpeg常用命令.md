# FFmpeg常用命令

### ```ffmpeg``` 

```-i "input.mp4" "output.mp4"``` ：导入&导出视频文件。使用绝对路径。如果文件名包含特殊含义字符，用半角双引号""来框住，如果没有就无所谓。单独使用 ```-i "[inputfile]"``` 可以查看文件信息。

```-c:v libx264``` ：使用h264编码。Codec:Video。等同于 ```-vcodec``` 。使用 ```-codecs``` 查看所有可使用编解码器，codec是COder&DECoder的缩写。

```-b:v 5000k``` ：输出码率5000kbps。Bitrate:Video。

```-r 24``` ：输出帧率24fps。frameRate。

```-crf 28``` ：恒定速率因子，ConstantRateFactor。 ```-crf 31``` 用于1080p通常被认为足够好了。libx264的默认值为28，范围是从0到51。

```-vf "transpose=1"``` ：顺时针旋转90°。VideoFilter。类似的有： ```"transpose=2"``` 为逆时针旋转90°； ```hflip``` 为水平翻转； ```vflip``` 为垂直翻转； ```transpose=3``` 等价于 ```"transpose=2,hflip"``` 为逆时针旋转90°后再水平翻转； ```"transpose=1,transpose=1"``` 为旋转180°。

```-vf crop=w:h``` ：画面裁剪。默认从画面中心裁剪，长与高像素比w:h

# 实例：

### 1、无损视频裁切：

从开始时间1分44秒，经历5分14秒（也就是到视频的6分58秒）。

```-ss``` ：开始时间，StartTime； ```-t``` ：持续时间，Time。

```
ffmpeg -ss 00:01:44 -t 00:05:14 -i "input.mp4" -vcodec copy -acodec copy "output.mp4"
```

由于视频采用帧间编码，所以不能精确到秒，只能从关键帧裁切。

### 2、无损视频拼接：

视频需要相同的编码格式和相同尺寸

```
ffmpeg -i concat:"1.mp4|2.mp4|3.mp4" -c copy output.mp4
```

或者使用：

```-f``` 指定封装格式； ```-safe 0``` 用于避免操作输入流的权限问题

```
ffmpeg -f concat -safe 0 -i list.txt -c copy output.mp4
```

需要合并的文件写进list.txt里，会输出拼合的文件output.mp4，注意要写清楚输入输出文件的路径

list.txt模板：

```
file '/home/user/Desktop/input1.mp4'

file '/home/user/Desktop/input2.mp4'

file '/home/user/Desktop/input3.mp4'
```

### 3、分离音视频流：

##### 只留视频：

```
ffmpeg -i input.mp4 -c:v copy -an video_output.mp4
```

##### 只留音频流：

```
ffmpeg -i input.mp4 -c:a copy -vn audio_output.mp3
```

### 4、常用视频压制：

```
ffmpeg -i input.mp4 -c:v libx264 -crf 31 output.mp4
```

如果手机竖着拍的，就加上 ```-vf "transpose=2"``` 