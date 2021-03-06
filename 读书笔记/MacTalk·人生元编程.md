

MacTalk·人生元编程
===
池建强

###创建智能文件夹
---

Finder提供了智能文件夹的功能，简单来说就是固化你的搜索条件，并形成文件夹存放在左侧边栏。

例如你想建一个文件大小大于1G的智能文件夹，使用快捷键`option+command+n`呼出新建智能文件夹界面，单击最右侧的加号，在条件选择第一栏选择"大小"，第二栏选择"大于"，第三栏输入"1G"，你就可以看到你的Mac上文件大于1G的列表，单击"存储"，命名后该文件夹就会出现在左侧边栏。随时单击随时动态监控自己的硬盘上有哪些超过1G的大文件。试试真他搜索条件吧! 

###Markdown 
---

我一般用以上文本编辑器进行编程和文字修改，说到大段写作，还得用Markdown软件，我常用的软件有以下三个。

* Day One:笔记类写作软件，支持大部分Markdown语法，按日期分类，同时支持标签、检索和导出功能，我的大部分文章都是用这个软件完成的。收费软件，可以直接从AppStore下载。 

* Byword:专注写作的Markdown文本编辑器，支持所有Markdown语法，提供简洁干净的写作界面，支持段聚焦、行聚焦相打印机模式。收费软件，可以直接从AppStore下载。 

* Mou:中国开发者编写的Markdown编辑器，支持一边写作一边预览，我常常用它来修改文章，实时预览效果，多种主题模式是Mou的特色。免费软件，接受赞助。

###1984
---

致疯狂的人  
他们特立独行  
他们桀骜不驯  
惹是生非  
他们格格不入  
他们用与众不同的眼光看得事物  
他们不喜欢墨守成规  
他们也不愿安于现状  
你尽可以认同他们，反对他们，颂扬或是诋毁他们  
但是唯独不能漠视他们  
因为他们改变了寻常世界  
他们推动人类向前迈进  
或许他们是别人眼里的疯子  
但他们却是我们眼中的天才  
因为只有那些疯狂到以为自己能够改变世界的人......  
才能真正改变世界

###维护你的Mac
---

Mac的OS X是一个使用起来非常简单的操作系统，一般情况下不需要装杀毒工具，大部分程序安装都非常简单，直接把后缀为app的程序拖进应用程序文件夹就可以了。但是，当你在使用系统时如果发现出现异常，那么就该进行日常维护了。

打开磁盘管理，选中你的系统盘，单击"修复磁盘权限"，对磁盘权限进行检查和修复。完成之后还可以手动执行维护脚本:

	sudo periodic daily 
	sudo periodic weekly
	sudo periodic monthly 

也可以一次全部执行:

	sudo periodic daily weekly monthly 

一般执行完这些操作后，你的Mac就会充满活力，可以继续上路了。这些操作可以定期执行。

###截图
---
OS X提供了非常方便的截图工具，你可以随时随地截取屏幕画面。

`shift+command+3` :全屏幕截图;  
`shift+command+4` :通过目标选取截图。

截取的图片默认存放在桌面上，以时间命名。系统默认截图格式是png，你可以通过如下命令修改截图文件类型，例如:

	defaults write com.apple.screencapture type -string JPEG

###Go2Shell
---
通过Finder浏览文件的时候，常常需要在浏览的文件目录中打开终揣进行操作，Go2Shell能够自动做到这一点。从App Store下载这个免费软件[Go2Shell](https:// itunes.apple.com/us/app/go2shell/id445770608?mt=12)。下载完成后从应用程序文件夹把Go2Shell拖到Finder工具栏上，然后随便进入一个目录，单击Go2Shell图标，即可打开终端进入该目录。

Go2Shell支持原生终端、iTerm2和xterm，在终端输入`open -a Go2Shell-args config`即可进入配置界面，选择你喜欢的终端。

###让Mac不进入休眠状态
---
如果你想离开电脑一段时间，又不想让电脑进入休眠状态，有个简单的命令可以帮助你做到这一点。在终端中输入:`pmset noidle`即可。只要该命令一直运行，Mac就不会进入睡眠状态。关掉终端或`ctrl+C`可以取消该命令。

`pmset`是OS X提供的命令行管理电源的工具，其功能远不止于此。

	pmset -9 #查看当前电源的使用方案
	sudo pmset -b displaysleep 5 #设置电池供电时，显示器5分钟内进入睡眠
	sudo pmset schedule wake "02/01/13 20:00:00" #设置电脑在2013年2月1日20点唤醒电脑
	......

感兴趣的可以使用`man pmset`查看详细信息。

###显示/隐藏桌面内容快捷键
---
我们经常会在桌面上堆满文件夹相文件，有时候会很方便，有时候会觉得很乱。其实我们可以通过以下命令来决定什么时候显示，什么时候隐藏:

	chflags hidden ~/Desktop/* //隐藏桌面内容
	chflags nohidden ~/Desktop/* //显示桌面内容

###显示/隐藏文件
---
在Finder中按`shift+command+.`键可以显示隐藏文件，想恢复原来的设置，再按一遍`shift+command+.`即可。

###隐藏程序
---
当我们不想在使用当前程序的时候看到其他程序的时候，可以使用快捷键`option+command+h`，这时除了你正在使用的程序，其他所有的程序都会被隐藏起来，有助于你专心工作。想切换到其他程序时，可以使用`command+tab`。 

###文件颜色标签的使用
---
OS X的Finder提供了颜色标签的功能，可以直接为文件和文件夹标记颜色。我在很长一段时间都没有注意到这个功能，一次偶然的机会开始使用颜色标记文件，感觉非常方便。

比如我会在Finder的主目录下用颜色标明最常访问的文件夹。如果是电子书，可以用颜色表示阅读状态，例如绿色表示正在阅读，灰色表示读完了，橙色表示待阅读，等等。大家可以根据自己的习惯使用颜色标签，提高效率。

###Mac的键盘 
---
很多人第一次用Mac的键盘时会发现，苹果也太抠门儿了，退格键没了，PageUp/PageDown/Home/End也没了。别担心，您不是还有`delete`键相上下左右方向键么?  
`delete`相对于退格键，`fn+delete`可以往前删，`fn+上下左右方向键`可以实现PageUp/PageDown/Home/End的功能，一个功能都不少。

```
电脑才不会跟人打交道，在这台坚硬的机器前，一切喜怒哀惧都是程序员心中的自言自语。
```
```
泰山崩于前，我依然沐浴更衣焚香沏茶。
```
```
但行好事，莫问前程;河狭水急，人急计生。
```
```
人比人死，货比货扔。
```
```
人总得去做选择，要么忙着去活，要么赶着去死(Get busy living, or get busy dying)。
```