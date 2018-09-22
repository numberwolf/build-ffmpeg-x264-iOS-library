-------------------------
> #define X264_POINTVER "0.142.x"
> ffmpeg-3.1.2

在FFmpeg使用到编码时要使用到libx264，通过FFmpeg+libx264可实现视频编码效果。
下面就是各个步骤：
1.x264库的编译
1) 使用最基本x264-ios脚本编译
首先我们从[http://www.videolan.org/developers/x264.html](https://link.jianshu.com?t=http://www.videolan.org/developers/x264.html)中下载x264的码源。

---------------------------
##### 特别注意！！ 请看这篇文章，ffmpeg对于x264版本是有要求的，貌似15+的就fail了直接，http://www.ffmpeg-archive.org/what-x264-version-to-build-ffmpeg-3-4-1-td4682514.html

###### 下载x264之后，运行以下version.sh检测一下你的版本
--------------------------

上面的步骤完成了后开始我们的编译：
进入脚本目录，将我们的下载的码源解压后，把它拷贝到脚本目录下，重命名为x264。

用终端进入脚本目录先执行./build-x264.sh运行完后在执行./build-x264.sh lipo这时目录中就会产生一个x264-iOS，scratch-x264，thin-x264几个文件。到这里x264库的编译就成功了。

2) 脚本集成x264库的编译
[https://github.com/tangyi1234/x264-iOS-build-script](https://link.jianshu.com?t=https://github.com/tangyi1234/x264-iOS-build-script)，下载集成脚本，下载页面中有脚本继承命令。下面就是具体操作。


* 打开终端进入cd到集成脚本目录，先执行`./build-x264.sh`执行完后在执行`./build-x264.sh lipo`

3.将libx264编译到FFmpeg
下载FFmpeg脚本[https://github.com/kewlbear/FFmpeg-iOS-build-script](https://link.jianshu.com?t=https://github.com/kewlbear/FFmpeg-iOS-build-script)。拷贝x264-iOS到[build-ffmpeg.sh](https://link.jianshu.com?t=http://build-ffmpeg.sh)脚本所在目录下，并重命名x264-iOS为fat-x264。之后进入脚本[build-ffmpeg.sh](https://link.jianshu.com?t=http://build-ffmpeg.sh)中修改两个地方

```
#X264=`pwd`/fat-x264
改为
X264=`pwd`/fat-x264

```

```
CFLAGS = “ $ CFLAGS -mios-version-min = $ DEPLOYMENT_TARGET -feded-bitcode”
修改为
CFLAGS = “ $ CFLAGS -mios-version-min = $ DEPLOYMENT_TARGET ”

```

修改完后终端进入脚本目录先执行./build-ffmpeg.sh这是一个漫长的过程执行完后./build-ffmpeg.sh lipo

Over.
