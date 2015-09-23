# 开始转码
## 简单的文件输入与输出

>	用 FFmpeg 来执行简单的格式转换出奇的简单！你不相信吗？来试一试就知道了！

首先你要准备一个视频文件，大部分你能见到的视频文件都可以，只要不是有 [DRM 保护](https://zh.wikipedia.org/wiki/%E6%95%B0%E5%AD%97%E7%89%88%E6%9D%83%E7%AE%A1%E7%90%86)的或者某某客户端的“专有格式”，基本上 FFmpeg 都能应付。不过作为练习，最好不要拿太大的文件，因为这样转换的时间会比较长。

我这里使用 [Tor](https://zh.wikipedia.org/wiki/Tor) 的介绍视频来作为例子，可以从[这个页面](https://blog.torproject.org/blog/releasing-tor-animation)来下载到，我所选择的是 [English HQ](https://media.torproject.org/video/2015-03-animation/HQ/Tor_Animation_en.mp4) 版本。当然，如我刚刚所说，你没有必要非得使用这个视频。

假设这个视频已经下载到了你的电脑硬盘中，并存放在 `/home/alex/Downloads/` 这个目录里面，而且 FFmpeg 已经[安装](02-download-and-install.md)到你的电脑中。那么现在[打开终端](03-execute.md#查看帮助)，然后使用 `cd` 命令转到文件所在的位置，比如在我的情况下，运行 `cd /home/alex/Downloads/` ，它不会有任何输出。

-	 **注意：** 如果文件路径包含空格或一些特殊字符，请使用半角引号（ `'` 或 `"` ）将路径名包起来，比如如果文件在 `/home/alex/path with space/` ，执行 `cd "/home/alex/path with space/"` 而 **不是** `cd /home/alex/path with space/` 。

-	 **注意：** 如果你使用的是 Microsoft&reg; Windows&reg; ，并且文件不在 C 盘，需要再“执行”一下盘符，比如如果文件存放在 `D:\\Downloads\` 里面，执行以下两条命令：
	
		cd D:\\Downloads\
		D:

`cd` 完了之后，如果你有强迫症想要检查一下是否真的已经切换到目标目录去了，可以运行 `ls` （ Linux, Mac OS X&reg; ）或 `dir` （ Microsoft&reg; Windows&reg; ）。只要显示出来的确实是那个目录里的文件，就说明没有问题，你可以放心继续。

![运行 cd 和 ls](image/cd-ls.png)

接下来输入 `ffmpeg` 但不要回车，我们要使用 `-i` [选项](03-execute.md#选项与参数)来指定输入文件。  
输入文件是什么？就是我们要转换的文件呀！比如我在此处要转换的文件叫做 `Tor_Animation_en.mp4` ，我就再往命令行中打 `-i Tor_Animation_en.mp4` 。

在指定了输入文件之后，我们还要指定一个输出文件，不然 FFmpeg 把转换出来的文件保存在哪儿呢？  
输出文件可以是任何名字，但它的后缀名很关键，[上一章](04-media-file-structure.md)已经讲过，后缀名通常就代表着文件的封装格式。在这个例子中，我想将视频转换为 [Matroska](https://zh.wikipedia.org/wiki/Matroska) 格式（俗称 MKV 格式），那么我输出文件的后缀名就得是 `.mkv` 。  
最终，我想将文件保存为 `tor.mkv` ，就在命令行后面直接加上这个文件名。

最后，我的命令行上有着这样一条命令：

	ffmpeg -i Tor_Animation_en.mp4 tor.mkv

-	 **注意：** 跟 `cd` 时的目录路径一样，如果文件名包含空格或一些特殊字符，也需要用半角引号将它们包裹起来。比如如果输入文件名叫 `input file.mp4` 且输出文件名叫 `output file.mkv` ，整条命令就得是 `ffmpeg -i "input file.mp4" "output file.mkv"` 。

按下回车吧！

虽然这一节的内容很长，不过你读过之后应该就会发现，这其实就是这么一条简单的命令。为了使大家更好理解，我才将这一节写的这么详细。

如果你使用的文件很小，而且电脑性能不是特别差，可能你还没有读完上一段话，就已经转换完成了。你的命令行窗口可能看起来像是这样：  
![转码成功完成](image/successful-completed.png)

你通常不必去管里面写的是什么，只要没出现红色的 `ERROR` ，一般就是没有问题地完成了。

现在，你闪闪发亮的输出文件已经保存在原来的目录中了。在我这里，这个 `tor.mkv` 就是转换后的输出文件。  
![在文件管理器中看到两个文件](image/files-in-explorer.png)

--------------------

## 指定编码器

FFmpeg 会自动判断输入文件的封装格式以及编码，并且根据输出文件的后缀名来判断其封装格式。同时， FFmpeg 也会根据该种封装格式的默认编码来决定输出文件的编码。

运行 `ffmpeg -help muxer=matroska` 就可以查看 Matroska 格式的默认编码了，我们可以在这条命令的输出中找到这样几行字：

	Muxer matroska [Matroska]:
	    Common extensions: mkv.
	    Mime type: video/x-matroska.
	    Default video codec: h264.
	    Default audio codec: vorbis.
	    Default subtitle codec: ass.

它们的意思是： Matroska 封装格式，通常的后缀名为 `mkv` ，[MIME](https://zh.wikipedia.org/wiki/%E5%A4%9A%E7%94%A8%E9%80%94%E4%BA%92%E8%81%AF%E7%B6%B2%E9%83%B5%E4%BB%B6%E6%93%B4%E5%B1%95) 为 `video/x-matroska` ，默认视频编码为 `h264` ，默认音频编码为 `vorbis` ，默认字幕编码为 `ass` 。如果你的[英语水平没问题](03-execute.md#中文是世界上最美的语言但是)，读懂这些将轻而易举。

[H264](https://zh.wikipedia.org/wiki/H.264/MPEG-4_AVC) 和 [Vorbis](https://zh.wikipedia.org/wiki/Vorbis) 都是两种十分流行的编码，大部分播放器都可以播放。不过，如果我想使用 Matroska 作为封装格式，但使用 [HEVC](https://zh.wikipedia.org/wiki/%E9%AB%98%E6%95%88%E7%8E%87%E8%A7%86%E9%A2%91%E7%BC%96%E7%A0%81) 作为视频编码，该怎么办呢？

快使用“帮助大法”，执行 `ffmpeg -help` 查看帮助！  
然后我们能看到这样一行：

	-vcodec codec       force video codec ('copy' to copy stream)

它告诉我们，使用 `-vcodec` 选项，可以指定视频编码器。如果指定 `copy` 将不会重新编码，而是直接把原来的媒体流拷贝过去。

现在我们可以在原来的命令（ `ffmpeg -i Tor_Animation_en.mp4 tor.mkv` ）的 **输出文件名之前** ，加上 `-vcodec hevc` ，这样 FFmpeg 就会使用 HEVC 而不是 H264 进行视频的编码。  
最后我们要使用的命令是这样的：

	ffmpeg -i Tor_Animation_en.mp4 -vcodec hevc tor.mkv

按下回车！

如果出现了 `File 'tor.mkv' already exists. Overwrite ? [y/N]` ，不要惊慌，他只是告诉你 `tor.mkv` 这个文件已经存在了，并问你是否要覆盖。如果你要覆盖原来的文件，按 `y` 再回车；如果你不想覆盖，按 `n` 回车，把文件名改一下，再重新执行命令。

这回的等待时间可能就长一些了，因为 HEVC 是一个压缩比更高的编码，需要的时间也长。

同样的，在 `ffmpeg -help` 的输出中，我们也可以找到 `-acodec` 选项，它是用来指定音频编码的。所以如果我想要以 Matroska 作为封装格式， HEVC 作为视频编码， [Opus](https://zh.wikipedia.org/wiki/Opus_codec) 作为音频编码，使用的命令会是这样的：

	ffmpeg -i Tor_Animation_en.mp4 -vcodec hevc -acodec opus tor.mkv

如果我想要直接拷贝媒体流到输出文件中而不重新进行编码（也就是只转换一下封装格式），在编码器的位置上写 `copy` 。比如 `ffmpeg -i Tor_Animation_en.mp4 -vcodec copy -acodec copy tor.mkv` ，因为这样不进行编码，所以通常会很快。

-	 **提示：** `-vcodec` 有一个缩写叫做 `-c:v` ， `-acodec` 有一个缩写叫做 `-c:a` 。  
	也就是说， `ffmpeg -i Tor_Animation_en.mp4 -vcodec hevc -acodec opus tor.mkv` 可以写为 `ffmpeg -i Tor_Animation_en.mp4 -c:v hevc -c:a opus tor.mkv` ，两者没有任何区别。  
	使用这样的小把戏可以省下打几个字母的时间。以后我举例也一直都会用这种简单的写法。

## 照它说的做

## 学会看输出
