# 转码时能顺便一起做的事情

虽然这篇教程的主要内容是视频转码，但除了将文件在各种封装格式、编码中转换以外，一些其他的调整也是很有用的。

在这一章中，我们将学到许多具有各种功能的[命令行选项](03-execute.md#options-and-arguments)，这些选项都需要加在整条命令的输出文件名之前。

万变不离其宗，在前面介绍的[查看帮助](03-execute.md#look-help)一节中学到的 `ffmpeg -help` 命令仍然是非常实用的，本章也将一直围绕它的输出来进行。所以，在开始阅读第一节之前，先打开终端，执行一下 `ffmpeg -help` 吧！

<a name="audio"></a>
## 音频

我们在 `ffmpeg -help` 的输出中能找到这样一段信息：

	Audio options:
	-aframes number     set the number of audio frames to output
	-aq quality         set audio quality (codec-specific)
	-ar rate            set audio sampling rate (in Hz)
	-ac channels        set number of audio channels
	-an                 disable audio
	-acodec codec       force audio codec ('copy' to copy stream)
	-vol volume         change audio volume (256=normal)
	-af filter_graph    set audio filters

这些就是关于音频的选项了，由于有些东西涉及的知识太多，我在这里只介绍比较常用且简单的 `-ar`, `-an`, `-vol` 这几个选项。（ `-acodec` 早就讲过了，不是吗？）

### -ar

如上面所说， `-ar` 选项后面还要跟一个叫 `rate` 的参数，不过参数叫什么名字对我们来说不重要，我们只要知道后面要有一个参数就可以了。这个参数是音频的[采样率](https://zh.wikipedia.org/wiki/%E9%87%87%E6%A0%B7%E7%8E%87)，以 Hz 为单位。

通常来说，采样率越大，音质越好。电话的采样率通常是 8000 Hz ，普通的录音笔通常是 32000 Hz ，一般的 MP3 音乐是 44100 Hz ，稍高品质的音乐是 48000 Hz ，再高的采样率我们平常就不容易接触到了。

以下是一个将音频文件 `input.mp3` 转换为 [Ogg](https://zh.wikipedia.org/wiki/Ogg) 封装格式， [Vorbis](https://zh.wikipedia.org/wiki/Vorbis) 编码，并且指定音频采样率为 32000 Hz 的例子：

	ffmpeg -i input.mp3 -c:a libvorbis -ar 32000 output.ogg

-	 **注意：** 在 FFmpeg 中使用 Vorbis 编码时，编码器应指定为 `libvorbis` 而不是 `vorbis` ，这是两个不同的编码器，而后者还处于不完善的状态。

-	 **提示：** 如果你喜欢的话，数字 `32000` 可以简写为 `32k` ，因为 "k" 就相当与“千”。

-	 **注意：** 采样率只能变小，不能变大。当然你要是指定一个比原来大的采样率也没人阻止你，不过音质不会有任何的提升就是了。原理跟你把一张分辨率很小的图片拉大一样，画质没有任何提升。

### -an

这个其实没什么好讲的，它就是在进行视频转码的时候，将音频给去除，这样就会得到一个没有声音的视频。

### -vol

这个选项有一个参数，用来指定相对与原来的文件的音量大小。不过注意，标准的音量并不是 100 ，而是 256 ，也就是说，我指定了 `-vol 256` 就是原来的音量不变（跟没指定一样）。

下面的例子是将音量减小为原来的一半：

	ffmpeg -i input.mp3 -c:a libvorbis -vol 128 output.ogg

<a name="video"></a>
## 视频

在 `ffmpeg -help` 的输出中，我们也能找到这样一段信息：

	Video options:
	-vframes number     set the number of video frames to output
	-r rate             set frame rate (Hz value, fraction or abbreviation)
	-s size             set frame size (WxH or abbreviation)
	-aspect aspect      set aspect ratio (4:3, 16:9 or 1.3333, 1.7777)
	-bits_per_raw_sample number  set the number of bits per raw sample
	-vn                 disable video
	-vcodec codec       force video codec ('copy' to copy stream)
	-timecode hh:mm:ss[:;.]ff  set initial TimeCode value.
	-pass n             select the pass number (1 to 3)
	-vf filter_graph    set video filters
	-ab bitrate         audio bitrate (please use -b:a)
	-b bitrate          video bitrate (please use -b:v)
	-dn                 disable data

同样的，实用为先，我在这里只挑 `-r`, `-s`, `-vn` 这几个选项来讲。

### -r

`-r` 选项可以指定视频的[帧率](https://zh.wikipedia.org/wiki/%E5%B8%A7%E7%8E%87)，其参数的单位是 Hz ，也就是我们平常所说的“帧每秒”（ FPS ）。比如 `-r 24` 即代表输出视频的帧率为每秒 24 帧。

当然，视频的帧率跟音频的采样率一样，只能变小不能变大。

### -s

这个选项可以指定视频的尺寸，以像素为单位。这个选项的参数由 `宽度x高度` 的格式填写。比如如果要把视频转为 720P （也就是宽度 1280 像素，高度 720 像素），就写上 `-s 1280x720` 。没错，中间用小写字母 `x` 分隔两个数字。

下面的例子会将输出文件视频的帧率指定为 15 帧每秒，画面尺寸 1280x720 ：

	ffmpeg -i input.mp4 -r 15 -s 1280x720 output.mkv

### -vn

与 `-an` 选项一样，在命令中加入了这个选项之后，视频内容便会被去除。也就是说，只把音频剥离出来。比如，把 `video.mp4` 这个视频中的音频提取出来，保存为 `audio.mp3` ，指定音频编码为 `mp3` ，将使用这样一个命令：

	ffmpeg -i video.mp4 -vn -c:a mp3 audio.mp3

-	 **提示：** MP3 封装格式的默认音频编码已经是 `mp3` ，我在这里写 `-c:a mp3` 其实是多此一举。

<a name="general"></a>
## 整体

除了仅仅针对媒体流的选项以外，还有一些针对整个媒体文件的调整选项。那么我们先在 `ffmpeg -help` 的输出中找出这样一段内容：

	Per-file main options:
	-f fmt              force format
	-c codec            codec name
	-codec codec        codec name
	-pre preset         preset name
	-map_metadata outfile[,metadata]:infile[,metadata]  set metadata information of 
	outfile from infile
	-t duration         record or transcode "duration" seconds of audio/video
	-to time_stop       record or transcode stop time
	-fs limit_size      set the limit file size in bytes
	-ss time_off        set the start time offset
	-sseof time_off     set the start time offset relative to EOF
	-seek_timestamp     enable/disable seeking by timestamp with -ss
	-timestamp time     set the recording timestamp ('now' to set the current time)
	-metadata string=string  add metadata
	-target type        specify target file type ("vcd", "svcd", "dvd", "dv" or "dv5
	0" with optional prefixes "pal-", "ntsc-" or "film-")
	-apad               audio pad
	-frames number      set the number of frames to output
	-filter filter_graph  set stream filtergraph
	-filter_script filename  read stream filtergraph description from a file
	-reinit_filter      reinit filtergraph on input parameter changes
	-discard            discard
	-disposition        disposition

我在这里将会挑选 `-c`, `-t`, `-ss`, `-metadata` 这几个选项来讲。

### -c

其实这个选项我们在[第 5 章第 2 节](05-start-converting.md#specify-codec)的最后已经讲过了，不过我觉得有必要再做一次详细的说明。

`-c` 选项用来指定输出文件的编码，但跟 `-vcodec` 和 `-acodec` 不同的是，它指定的是全部媒体流的编码而不是单独一个视频流或音频流。在通常情况下，这是行不通的，因为视频编码和音频编码是两种不同的东西，怎么能是同一个呢？

但是，我们可以通过在 `-c` 后面紧挨着加上 `:v` 成为 `-c:v` 来表示指定视频编码，紧挨着加上 `:a` 成为 `-c:a` 来表示指定音频编码。也就跟 `-vcodec` 和 `-acodec` 一样了。不过 `-c:a`, `-c:a` 的写法比 `-vcodec`, `-acodec` 的写法要短，所以我喜欢用前者。

当然，单独的 `-c` 也是有用的，有什么用呢？

还记得在编码器的地方指定 `copy` 来让 FFmpeg 不重新进行编码吗？众所周知，大部分视频或音频编码都是[有损压缩](https://zh.wikipedia.org/wiki/%E6%9C%89%E6%8D%9F%E6%95%B0%E6%8D%AE%E5%8E%8B%E7%BC%A9)，重新进行一次编码不但费时费力，还会产生无法挽回的画质/音质损失，损失一两次通常是人类很难判别的，但是次数多了差别就大了。所以，我们要尽量避免重新编码，能用 `copy` 作为“编码器”的时候就尽量使用它。

让视频不重新编码的时候使用 `-c:v copy` ，让音频不重新编码的时候使用 `-c:a copy` 。那么在两个都要不重新编码的时候，就不用把这两条选项都写上去了，只要 `-c copy` 就足够。

下面是一些例子：

1.	将视频尺寸转换为 `1280x720` ，其他不变。  
	因为视频的尺寸变了，所以视频不得不重新编码，但音频不用。
	
		ffmpeg -i input.mp4 -c:v h264 -c:a copy -s 1280x720 output.mp4

2.	将音频的编码转换为 `libvorbis` ，其他不变。  
	音频的编码肯定得变，但是视频不用。
	
		ffmpeg -i input.mp4 -c:v copy -c:a libvorbis output.mp4

3.	仅仅将 MP4 封装格式转换为 Matroska 封装格式。  
	只是封装格式变了，视频和音频都不需要重新编码。
	
		ffmpeg -i input.mp4 -c copy output.mkv

### -t

这个选项用来指定输出文件的持续时间，以秒为单位，比如我想截取 `full.mp4` 这个视频的前 30 秒并保存为 `segment.mp4` ，就可以使用这个命令：

	ffmpeg -i full.mp4 -c copy -t 30 segment.mp4

-	 **注意：** 看到了 `-c copy` 了吗？因为我们只是进行截取，所以不需要进行重新编码。能不重新编码就尽量不要重新编码。

这个选项的参数以秒为单位，但这并不意味着 5 分钟你就得写 `300` ， 1 个小时你就得写 `3600` ， 1 小时 23 分钟 45 秒你就得先拿出计算器算出 1&#x00d7;3600+23&#x00d7;60+45=5025 再写上 `5025` 。  
事实上，你只要写 `5:00` 就可以表示 5 分钟， `1:23:45` 就可以表示 1 小时 23 分钟 45 秒。

你也可以写小数点，比如 `10.0268` 或者 `1:23:45.678` 。

### -ss

这个选项用来指定输出文件相对于输入文件的开始时间，比如我想把 `full.mp4` 这个视频的前 30 秒剪掉并把剩下的保存为 `segment.mp4` ，就可以使用这个命令：

	ffmpeg -i full.mp4 -c copy -ss 30 segment.mp4

`-ss` 选项也可以跟 `-t` 选项配合使用以截取媒体文件的一部分，比如如果我想截取 `full.mp4` 的 12 分 25 秒至 20 分 27 秒，保存为 `segment.mp4` ，使用这条命令。

	ffmpeg -i full.mp4 -c copy -ss 12:25 -t 8:02 segment.mp4

-	 **注意：** `-t` 选项后面的参数并不是结束时间而是持续时间，所以在上面的例子中我写的不是 `20:27` 而是 20:27-12:25 的结果， `8:02` 。

### -metadata

这个选项说的很明白了，它所更改的就是输出文件的[元数据](https://zh.wikipedia.org/wiki/%E5%85%83%E6%95%B0%E6%8D%AE)，比如一首歌的标题、艺术家、专辑。比如 `-metadata title="我是标题"` 就会把输出文件的标题元数据改为 `我是标题` 。 `-metadata` 选项可以多次指定以更改多个元数据。

举个例子，把 `no metadata.mp3` 的标题改成 `一首歌` ，艺术家改成 `一位艺术家` ，专辑改成 `一张专辑` ，然后保存为 `with metadata.mp3` ：

	ffmpeg -i "no metadata.mp3" -c copy -metadata title="一首歌" -metadata artist="一位艺术家" -metadata album="一张专辑" "with metadata.mp3"

-	 **提示：** 还记得吗？在文件名包含空格或其他特殊字符的时候，必须用半角双引号包起来。

---------------------------

>	我在命令中所写的选项和参数，顺序有关系吗？

这样的问题可能发自一个对命令行不熟悉的用户。那么我就来解答一下：在 FFmpeg 中，以我们目前的知识，除了 `-i 输入文件名` 必须在仅次于 `ffmpeg` 的最前面以及输出文件名必须在最后面以外，选项的顺序没有关系。

也就是说，以下两条命令是没有任何区别的。

	ffmpeg -i input.mp4 -c:v vp9 -c:a opus -s 1280x720 -ss 10 -t 1:00 output.webm
	ffmpeg -i input.mp4 -t 1:00 -c:v vp9 -s 1280x720 -c:a opus -ss 10 output.webm

但是注意了，一个选项跟这个选项的的参数是不可分开的，也就是说，音频编码必须跟在 `-c:a` 后面，持续时间必须跟在 `-t` 后面……下面这条命令是 **错误** 且 **无法** 被正常运行的：

	ffmpeg -i input -c:v -ss -t 10 -ss -c:a 1280x720 vp9 1:00 opus -s output.webm

看完了这些说明，我想你就应该能够熟练地掌握命令行的规则了。后面的内容依然还在编写中，如果想要获知最新的更新，请关注这个计划的 [GitHub Repository](https://github.com/FiveYellowMice/how-to-convert-videos-with-ffmpeg-zh) 。

对了，也看一看[最后一章](10-write-in-end.md)。
