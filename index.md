# 如何使用 FFmpeg 进行视频转码

![CC-BY-SA](image/by-sa.png)  
本作品采用知识共享 署名-相同方式共享 4.0 国际 许可协议进行许可，你可以在署名并采用相同条款的情况下自由复制、传播、再演绎本作品而无需通知作者。访问 <http://creativecommons.org/licenses/by-sa/4.0/> 查看该许可协议。

## 目录
1.	[写在前面](01-write-in-front.md)
	1.	[丑话说在前头](01-write-in-front.md#丑话说在前头)
	2.	[FFmpeg 是什么，我为什么要用它？](01-write-in-front.md#ffmpeg-是什么我为什么要用它)
2.	[下载与安装](02-download-and-install.md)
	1.	[Linux](02-download-and-install.md#linux)
	2.	[Mac OS X&reg;](02-download-and-install.md#mac-os-x)
	3.	[Microsoft&reg; Windows&reg;](02-download-and-install.md#microsoft-windows)
	4.	[手机、平板、树莓派……](02-download-and-install.md#手机平板树莓派)
3.	[运行](03-execute.md)
	1.	[是这个黑黑的窗口吗？](03-execute.md#是这个黑黑的窗口吗)
	2.	[查看帮助](03-execute.md#查看帮助)
	3.	[“选项”与“参数”](03-execute.md#选项与参数)
	4.	[支持哪些格式？](03-execute.md#支持哪些格式)
	5.	[中文是世界上最美的语言，但是……](03-execute.md#中文是世界上最美的语言但是)
4.	[媒体文件的结构](04-media-file-structure.md)
5.	开始转码
	1.	简单的文件输入与输出
	2.	指定编码器
	3.	照它说的做
	4.	学会看输出
6.	转码时能顺便一起做的事情
	1.	音频
	2.	视频
	3.	整体
7.	字幕
	1.	作为字幕流
	2.	编入视频流
8.	不同编码器特有的设定
	1.	H264
	2.	学会看文档
9.	不仅能转码
10.	写在最后
