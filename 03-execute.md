# 运行
## 1.	是这个黑黑的窗口吗？

如果你是一名 Windows&reg; 用户，在第一次运行 ff-promt.bat 的时候，也许会被吓一跳，因为此时出现在屏幕前的，是一个黑底白字——就像在黑客电影中所见到的那样的窗口。  
![ff-prompt](image/windows-ff-prompt.png)

>	「什么情况？我的电脑坏了？」

你此时心中可能会这样想。但是实际上我想告诉你，你的电脑并没有坏，这个窗口是接下来你要经常面对的东西了。  
别害怕，这并不是什么只有在电影中才能看见的高级玩意儿，在十几至二十几年前，大部分的电脑都是这样子。

>	「可是现在都什么时代了，为什么还要使用这种老土的东西？」

事实上，即使在今天，许多人也在使用它来完成大部分的任务，许多事情还只能靠它来完成。  
图形界面的发明给是计算机界的一大进步，带来了许多好处，但同时的，图形化的东西也有许多缺点。比如，找一个功能需要很多次点击，程序的开发也要消耗许多精力在“如何设置一个好的图形界面”上，图形界面还促使了鼠标手的产生。

我们不得不承认，许多任务，用命令行来完成更高效。 FFmpeg 很好的诠释了这一点。  
命令行没什么好怕的，我天天用呢，如果哪天它突然消失了，我还不知道我该如何使用我的电脑呢。

好了我觉得我在这节内容上耗费太多时间了，本文讲的是 FFmpeg 的用法而不是命令行的优势，再多讲就跑题了。如果你还不服，或者感兴趣，[这篇文章](http://os.51cto.com/art/201007/215287.htm)也许挺适合你。

------------------------

## 2.	查看帮助

首先，打开终端。

-	Linux
	
	我想我不用说了，你们都会。

-	Mac OS X&reg;
	
	点 Dock 中的 Dashboard ，找到 Terminal ，点它。

-	Microsoft&reg; Windows&reg;
	
	按 Win + R ，输入 `cmd` ，回车。

然后，执行以下命令：

	ffmpeg -version

你可以看到像这样的一些输出：

	ffmpeg version 2.7.2 Copyright (c) 2000-2015 the FFmpeg developers
	built with gcc 5.2.0 (GCC)
	configuration: --prefix=/usr --disable-debug --disable-static --disable-strippin  
	g --enable-avisynth --enable-avresample --enable-fontconfig --enable-gnutls --en  
	able-gpl --enable-libass --enable-libbluray --enable-libfreetype --enable-libfri  
	bidi --enable-libgsm --enable-libmodplug --enable-libmp3lame --enable-libopencor  
	e_amrnb --enable-libopencore_amrwb --enable-libopenjpeg --enable-libopus --enabl  
	e-libpulse --enable-libschroedinger --enable-libsoxr --enable-libspeex --enable-  
	libssh --enable-libtheora --enable-libv4l2 --enable-libvorbis --enable-libvpx --  
	enable-libwebp --enable-libx264 --enable-libx265 --enable-libxvid --enable-share  
	d --enable-version3 --enable-x11grab
	libavutil      54. 27.100 / 54. 27.100
	libavcodec     56. 41.100 / 56. 41.100
	libavformat    56. 36.100 / 56. 36.100
	libavdevice    56.  4.100 / 56.  4.100
	libavfilter     5. 16.101 /  5. 16.101
	libavresample   2.  1.  0 /  2.  1.  0
	libswscale      3.  1.101 /  3.  1.101
	libswresample   1.  2.100 /  1.  2.100
	libpostproc    53.  3.100 / 53.  3.100

