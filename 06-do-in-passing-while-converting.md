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

-	 **提示：** `.mp3` 封装格式的默认音频编码已经是 `mp3` ，我在这里写 `-c:a mp3` 其实是多此一举。

<a name="general"></a>
## 整体
