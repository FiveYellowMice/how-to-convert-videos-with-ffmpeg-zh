# 字幕

在观看非母语语言的视频的时候，[字幕](https://zh.wikipedia.org/wiki/%E5%AD%97%E5%B9%95)是非常有用的东西。我们在网上能找到许多带字幕的视频，这些字幕很多时候已经跟视频融为一体了。不过有时候，我们还是能找到单独的字幕文件，这些字幕文件通常以 `.srt` 或 `.ass` 作为后缀名，且能被文本编辑器打开。

要让这些字幕在播放视频的时候显示在屏幕上，我们得让播放器除了打开视频文件以外，还得加载对应的字幕文件。许多播放器也会自动加载与视频文件名相似的字幕文件或是从网上寻找字幕，不过那是另外一回事了，每个播放器也不一样。

我在这里还是拿第 5 章中所提到的 [Tor 介绍视频](https://blog.torproject.org/blog/releasing-tor-animation)来做例子，我已经下载了 [English HQ](https://media.torproject.org/video/2015-03-animation/HQ/Tor_Animation_en.mp4) 版本的视频，现在我还要下载 [Chinese (China)](https://media.torproject.org/video/2015-03-animation/subs/Tor_animation.zh-CN.srt) 版本的字幕。当然，你没有必要用我使用的例子做试验。

把视频和字幕放在一个目录中，打开视频，然后在播放器中加载字幕文件，就可以看到字幕在播放视频的时候出现在屏幕上了。

但是这样做很麻烦，也很容易在拷贝或下载时忘记。所以，使用 FFmpeg 将字幕放到视频里吧！

<a name="as-subtitle-stream"></a>
## 作为字幕流

如[第 4 章](04-media-file-structure.md)中所说，媒体文件是由多个 **媒体流** 组成的，我们已经对视频流和音频流很熟悉了，但在这一节，我们将认识另一种媒体流——字幕流。 **字幕流独立于视频流** ，所以它可以随时开关，就像声音可以被静音一样。

字幕流跟其他媒体流一样，有各种编码，常见的编码有 [SubRip](https://en.wikipedia.org/wiki/SubRip) （作为独立文件时后缀名为 `.srt` ）和 [ASS](https://zh.wikipedia.org/wiki/SubStation_Alpha#Advanced_SubStation_Alpha.EF.BC.88ASS.E5.AD.97.E5.B9.95.EF.BC.89) （作为独立文件时后缀名为 `.ass` ）。运行 `ffmpeg -codecs` 可以查看 FFmpeg 支持的所有编码，而其中第 3 列为 `S` 的就是字幕编码。

字幕文件其实也能够算是媒体文件，只不过它不包含视频流和音频流，而是只包含了字幕流。

所以，如果我把只有视频流和音频流的媒体文件 `Tor_Animation_en.mp4` 与只有字幕流的媒体文件 `Tor_animation.zh-CN.srt` 合并到一起，就会得到一个有视频流、音频流和字幕流的媒体文件了。

在 FFmpeg 中，这样做很简单，只要把要合并的两个文件都作为输入文件就可以了，也就是在 `ffmpeg` 后面写上 `-i Tor_Animation_en.mp4 -i Tor_animation.zh-CN.srt` 。 FFmpeg 会将两个输入文件中的媒体流放都到其输出文件中去。

但是并不是所有的封装格式都支持字幕流，比如常见的 MP4 格式就不支持。要查看一个封装格式是否支持字幕流，请运行 `ffmpeg -help muxer=封装格式` ，如果输出中有 `Default subtitle codec:` 这样一行，即代表此封装格式支持字幕流。如果输出文件的封装格式不支持字幕流， FFmpeg 会忽略掉它或者报错。

-	 **提示：** 顺带一提， Matroska 和 WebM 封装格式都是支持字幕流的。

在[第 5 章第 4 节](05-start-converting.md#learn-to-look-output)中，我们知道了可以在 FFmpeg 开始转码时查看媒体流的分布（ Stream mapping ），我在执行 `ffmpeg -i Tor_Animation_en.mp4 -i Tor_animation.zh-CN.srt Tor_Animation_subtitled.mkv` 的时候，就会看到这样的输出：

	Stream mapping:
	  Stream #0:0 -> #0:0 (h264 (native) -> h264 (libx264))
	  Stream #0:1 -> #0:1 (aac (native) -> vorbis (libvorbis))
	  Stream #1:0 -> #0:2 (subrip (srt) -> ass (native))

它很直观地告诉我，在本次操作中， 0 号输入文件（也就是 `Tor_Animation_en.mp4` ）中的 0 号媒体流变成了 0 号输出文件的 0 号媒体流， 0 号输入文件中的 1 号媒体流变成了 0 号输出文件的 1 号媒体流， 1 号输入文件（也就是 `Tor_animation.zh-CN.srt` ）的 0 号媒体流变成了 0 号输出文件的 2 号媒体流。编码的转换也被清晰地显示了出来。

因为字幕流也是媒体流，也有各种编码，所以，我们也可以通过 `-scodec` 或 `-c:s` 选项来指定字幕流的编码。这个例子可以让 FFmpeg 复制视频流和音频流，而将字幕流转换为 `ass` 编码：

	ffmpeg -i Tor_Animation_en.mp4 -i Tor_animation.zh-CN.srt -c:v copy -c:a copy -c:s ass Tor_Animation_subtitled.mkv

同样的， `-c` 选项除了会影响到视频流和音频流以外，也会影响到字幕流，也就是说，指定 `-c copy` 也会让 FFmpeg 不对字幕流进行重新编码。

你甚至可以将字幕文件作为单独的输入文件！也就是对字幕文件进行转码，比如 `ffmpeg -i Tor_animation.zh-CN.srt Tor_animation.zh-CN.ass` 就会将 SubRip 字幕转换为 ASS 字幕。（因为 ASS 封装格式的默认字幕编码就是 `ass` ，所以你在这条命令中不用写 `-c:s ass` ）

<a name="encode-to-video"></a>
## 编入视频流
