# 写在前面

<a name="unpleasant-words-in-front"></a>
## 丑话说在前头

我知道这样可能使你的心情不好，但是为了防止我受到不明不白的诋毁，我还是得写下这一节。

如果你心中怀着以下想法之一，并且觉得这样是十分正确的，请点击右上角的 X ：

-	我 XXXX 用的挺好的，管它做了什么事，能用就行。
-	这么多人用的东西竟然没有中文，看来它根本不重视中国市场。
-	好麻烦啊，我只想要现成的。
-	上个世纪八国联军……
-	你是中国人不？是就支持国产，抵制外国货！
-	怎么这么多链接打不开？
-	啊，f墙？麻不麻烦啊，你直接把内容复制过来呗，我懒。

没符合上面中的任何一条？太好了！你应该是个拥有逻辑思维的人，我相信大部分人都是。

符合吗？那抱歉了，我建议你现在就点右上角的 X 。当然你要是愿意看下去我也管不着，只是最好别发一些激动的评论，否则我会尽量让你 **圆润离开** 。

说完了上面不适合的，我在来说说适合的人群：

-	想学会怎么转视频格式、编码的人。
-	想在视频网站上做出优秀视频的人。
-	视频资源收集控。
-	想了解关于数字媒体的知识，但以前从未接触过的人。
-	知道国产毒瘤们的恶劣事迹，但苦于找不到替代品的人。
-	不希望自己的东西被别人——或者别人编写的程序——掌控的人。

其实不符合也没关系， **只要你有兴趣，我当然欢迎你继续阅读下去！**

<a name="what-is-ffmpeg-why-use-it"></a>
## FFmpeg 是什么，我为什么要用它？

[FFmpeg][] 是一个多媒体编解码器库，并提供了命令行前端。许多软件都使用了 FFmpeg 来进行音频和视频的编解码，特别是像 [MPlayer][] 这样的多媒体播放器。  
FFmpeg 还是一个[自由软件][]，因为自由，所以其他人可以非常方便的在他们的软件中使用 FFmpeg 的东西。如果没有 FFmpeg ，许多播放器都要自己重新写解码器。有了 FFmpeg ，那些游戏开发者只要在他们的程序中包含 FFmpeg 的视频解码模块就可以播放视频了，而将更多的精力放在游戏本身内容上面。

这份自由是来之不易的，然而它也是脆弱的。 FFmpeg 作为一个遵循 [GNU 宽通用公共许可证][]（简称 LGPL）的软件，任何人都可以获取它的代码并放入自己的程序中，但是有一个限制，那就是这样的程序必须也采用 LGPL ，也意味着必须开放源代码。  
但是一些软件并没有这么做，这当然是无法肯定的，拿了人家的代码，自然就得听人家的规矩。于是就有一个[耻辱柱][]，记下志愿者们发现的不遵守协议的软件。

让我们来看一下这个耻辱柱吧。  
里面出现了 Baofeng Storm ，也就是大家所熟知的**暴风影音**。  
还有 QQPlayer ，也就是 **QQ 影音**。  
当然也少不了广为人知的 Format Factory ，也就是**格式工厂**。

再看看[这篇文章](https://www.byvoid.com/zhs/blog/qq-player-ffmpeg-gpl)，他分析的比我透彻的多。  
看到这些，你还能淡定地用着它们吗？  
播放器的话，有 [SMPlayer][] 和 [VLC][] 这两款开源免费的播放器。哦对了，播放音乐的话，也少不了 [Audacious][] 。

但是转码软件就没这么简单了，它的选择似乎要少得多。  
事实上，不论是像格式工厂这样违反 LGPL 的转码软件，还是像 [MeGUI][] 这样遵守 LGPL 的软件，市面上能见到的大多数转码软件都是拿着 FFmpeg 的核心，套了一层自己的皮而已。  
那为何不用最纯正的 FFmpeg 呢！

不但有着最大的定制性，还有着最轻量的前端。  
[命令行](03-execute.md#this-black-window)的操作界面，也能够写入脚本中，高效的完成批量任务。  
我想你已经迫不及待了，那么就开始阅读[第 2 章](02-download-and-install.md)吧！

[FFmpeg]:	https://zh.wikipedia.org/wiki/FFmpeg
[MPlayer]:	https://zh.wikipedia.org/wiki/MPlayer
[自由软件]:	https://zh.wikipedia.org/wiki/%E8%87%AA%E7%94%B1%E8%BD%AF%E4%BB%B6
[GNU 宽通用公共许可证]:	https://zh.wikipedia.org/wiki/GNU%E5%AE%BD%E9%80%9A%E7%94%A8%E5%85%AC%E5%85%B1%E8%AE%B8%E5%8F%AF%E8%AF%81
[耻辱柱]:	https://github.com/FFmpeg/web/blob/master/src/shame
[SMPlayer]:	http://smplayer.sourceforge.net/zh/info
[VLC]:	http://www.videolan.org/vlc/
[Audacious]:	http://audacious-media-player.org/
[MeGUI]:	http://sourceforge.net/projects/megui/
