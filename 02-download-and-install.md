# 下载与安装
## Linux

得益于 Linux 上强大的包管理系统，在 Linux 中安装 FFmpeg 非常简单。但由于各种发行版采用的包管理器不同，安装时需要执行的命令也不同，以下列举三种最常见的包管理器安装 FFmpeg时所需的命令，全部需要以 root 账户执行：

-	Debian, Ubuntu, Linux Mint  
	
		apt-get install libav-tools
	
	**Debian 及其衍生版用户注意：**因为一些历史原因， Debian 及其衍生版上是没有一个叫做 `ffmpeg` 的软件包的，确认代之的是 `libav-tools` ，需要执行的命令也是 `avconv` 而不是 `ffmpeg` ，以后将不会重复说明！请将后面的 `ffmpeg` 命令自行脑补成 `avconv` 。

-	Fedora, CentOS, RHEL
	
		yum install ffmpeg
	
	Fedora 22 及更高版本请用 `dnf` 代替 `yum` 。

-	Arch Linux, Manjaro
	
		pacman -S ffmpeg

实际上，在你看到这篇文章之前，你的电脑中很可能已经安装好了 FFmpeg ，在这种情况下，包管理器会提示已经安装。

------------------

## Mac OS X&reg;

*由于作者缺少对此操作系统的了解，所写的信息可能不准确，本节内容或许需要了解它的人对其进行完善和修改。*

在 Mac OS X&reg; 上安装 FFmpeg 有两种方式：第三方包管理器以及手动安装。

### 第三方包管理器

如果你的电脑中已经安装了 [Homebrew](http://brew.sh/) ，可以使用以下命令安装：

	brew install ffmpeg

如果没有安装 Homebrew ，可以执行以下命令来安装 Homebrew ，再执行上面的命令安装 FFmpeg ：

	ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

### 手动安装

访问 <http://evermeet.cx/ffmpeg/> ，你会看到 FFmpeg 标签下有一左一右两个绿色的下载按钮，左边版本更新，右边则更稳定，凭你的喜好，点哪个都可以。

然后解压这个压缩文件，你能够看到 ffmpeg 这一个文件，接下来打开终端， `cd` 到文件存在的目录，执行下列命令：

	sudo cp ffmpeg /usr/local/bin/
	sudo chmod 755 /usr/local/bin/ffmpeg

此时在终端中执行 `ffmpeg` ，如果出来的内容不是 `bash: ffmpeg: command not found` ，就说明安装成功了！

------------------

## Microsoft&reg; Windows&reg;

首先你需要知道 [你的电脑是 32 位还是 64 位](https://support.microsoft.com/zh-cn/kb/827218)。

然后访问 <http://ffmpeg.zeranoe.com/builds/> ，你可以看到许多灰色的按钮。如果你的电脑是 32 位，点最上面一行左边的按钮 "Download FFmpeg git-xxxxxxx 32-bit Static" ，如果是 64 位，点右边的 "Download FFmpeg git-xxxxxxx 64-bit Static" 。解压。

双击 ff-prompt.bat ，如果出现了如下的界面，并且最后一行可以进行输入，则表示没有问题。  
![ff-prompt](image/windows-ff-prompt.png)

它是一个绿色软件，你可以直接在这个窗口中执行接下来会讲到的命令。但为了方便，我推荐你进行“手动安装”。
双击解压出来的 bin 目录，可以看到 3 个 .exe 文件，将它们选中，复制到 `C:\\Windows\system32\` 中，此操作可能需要管理员权限。  
然后在[命令提示符](https://zh.wikipedia.org/wiki/%E5%91%BD%E4%BB%A4%E6%8F%90%E7%A4%BA%E5%AD%97%E5%85%83)中输入 `ffmpeg` ，如果出来的不是 `"ffmpeg" 不是一个文件或内部命令`，则说明安装成功！

----------------------

## 手机、平板、树莓派……

虽然理论上 FFmpeg 可以在移动平台运行，但是目前移动端上十分缺乏此类应用。封闭的 iOS 就不提了，在 Android 上有一个[以 FFmpeg 为核心的转码应用](https://play.google.com/store/apps/details?id=com.silentlexx.ffmpeggui)，但是功能严重不全，操作方式也大不相同。

所以转码工作最好还是在电脑上进行。

[树莓派](https://zh.wikipedia.org/wiki/%E6%A0%91%E8%8E%93%E6%B4%BE)是一个特殊的存在，它并不是一台如我们想象中一样的 x86 电脑，但是它可以当作一台性能和能耗较低的电脑来使用。它预装的操作系统是 Raspbian , Debian 的一个衍生版，在它上面的安装请参考上面关于 Linux 的说明。

------------------------

安装好了，一切就绪？那么开始[第 3 章](03-execute.md)的阅读吧！