# 如何使用 FFmpeg 进行视频转码

![CC-BY-SA](image/by-sa.png)  
本作品采用知识共享 署名-相同方式共享 4.0 国际 许可协议进行许可，你可以在署名并采用相同条款的情况下自由复制、传播、再演绎本作品而无需通知作者。访问 <http://creativecommons.org/licenses/by-sa/4.0/> 查看该许可协议。

## 欢迎

FFmpeg 是一个使用广泛的开源多媒体编解码器，其一大用途就是进行音频或视频的编码及格式转换。

FFmpeg 并不像它表面看上去那么高端，那么难。只是中文的资料实在太少，才造成了这样的表象。所以，我决定动手开启这个计划，为中文用户提供一个更简单易学的 FFmpeg 教程。

不过本教程只能让你成为 FFmpeg 用户，不能让你成为 FFmpeg 专家，专家的那些东西我也不明白。不过就大多数情况而言，你一辈子也用不到那些专家的东西。即使偶然用到， Google 足够作为你的伙伴了。

那么没有问题的话就[从第一章开始阅读](01-write-in-front.md)吧！

## 目录

没有链接的章节是在此版本中还未写完的部分，如果想要查看最新的开发版本，请访问这个计划的 [GitHub Repository](https://github.com/FiveYellowMice/how-to-convert-videos-with-ffmpeg-zh) 。

1.	[写在前面](01-write-in-front.md)
	1.	[丑话说在前头](01-write-in-front.md#unpleasant-words-in-front)
	2.	[FFmpeg 是什么，我为什么要用它？](01-write-in-front.md#what-is-ffmpeg-why-use-it)
2.	[下载与安装](02-download-and-install.md)
	1.	[GNU/Linux](02-download-and-install.md#gnu-linux)
	2.	[Mac OS X&reg;](02-download-and-install.md#mac-os-x)
	3.	[Microsoft&reg; Windows&reg;](02-download-and-install.md#microsoft-windows)
	4.	[手机、平板、树莓派……](02-download-and-install.md#phone-tablet-rasppi)
3.	[运行](03-execute.md)
	1.	[是这个黑黑的窗口吗？](03-execute.md#this-black-window)
	2.	[查看帮助](03-execute.md#look-help)
	3.	[“选项”与“参数”](03-execute.md#options-and-arguments)
	4.	[支持哪些格式？](03-execute.md#what-formats-supported)
	5.	[中文是世界上最美的语言，但是……](03-execute.md#chinese-is-most-beautiful-but)
4.	[媒体文件的结构](04-media-file-structure.md)
5.	[开始转码](05-start-converting.md)
	1.	[简单的文件输入与输出](05-start-converting.md#simple-io)
	2.	[指定编码器](05-start-converting.md#specify-codec)
	3.	[照它说的做](05-start-converting.md#do-what-it-says)
	4.	[学会看输出](05-start-converting.md#learn-to-look-output)
6.	[转码时能顺便一起做的事情](06-do-in-passing-while-converting.md)
	1.	[音频](06-do-in-passing-while-converting.md#audio)
	2.	[视频](06-do-in-passing-while-converting.md#video)
	3.	[整体](06-do-in-passing-while-converting.md#general)
7.	[字幕](07-subtitles.md)
	1.	[作为字幕流](07-subtitles.md#as-subtitle-stream)
	2.	[编入视频流](07-subtitles.md#encode-to-video)
8.	[不同编码器特有的设定](08-differente-encoders-special-options.md)
	1.	H264
	2.	学会看文档
9.	不仅能转码
10.	[写在最后](10-write-in-end.md)
