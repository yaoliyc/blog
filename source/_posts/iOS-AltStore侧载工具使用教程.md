---
title: iOS AltStore侧载工具使用教程
date: 2025-05-18 10:04:02
tags: [AltStore]
categories: [AltStore]
---

# iOS AltStore侧载工具使用教程


---
-   **iOS AltStore侧载工具使用教程**
    

![](IMG_4839.jpeg.webp)

终于开始写iOS侧载了（好耶）

目前网上的教程还是有点乱七八糟的，也不乏那些机翻的教程（不过我个人觉得我的写作风格也有点机翻的味道?）而且有一些AltStore的新功能网上讲的还是有点少。（总之还是以个人整理为主）

那么就不多逼逼，马上开始介绍。


## Windows食用方法

“AltStore”虽然是一个在iOS上跑的软件，但是想正常使用还是需要电脑端AltServer的配合。

首先我们前往[AltStore官网](https://altstore.io/)，然后点那个大大的“Get AltStore”：

![Altstore官网](图片1.webp)

话说AltStore网站还更新了

然后我们选择对应你系统的版本下载：

![AltStore选择不同的版本下载。](图2.webp)

\[warning\]AltStore是不支持Windows 7/8.x的，虽然可以跑，但是100%会报错。\[/warning\]

接下来双击打开刚刚下载好的“altinstaller.zip”打开：

![AltStore的Windows安装程序。](图3.webp)

两个文件的功能是一样的，任意选择一个打开即可。（为了写这篇东西我还特意把AltServer卸了重装?）

![AltServer安装1](图4.webp) ![AltServer安装2](图5.webp)

跟正常安装软件没有区别，一路“Next”就行。

然后就可以在开始菜单里看到AltServer的图标，点击运行。

这时候会提示驱动不完整（因为我已经装过驱动了，所以这里给不了图）。我们需要安装iTunes和iCloud。切记不能从Microsoft store下载，需要从苹果官网下载.exe格式的安装包。

iTunes下载（64位）：[https://www.apple.com/itunes/download/win64](https://www.apple.com/itunes/download/win64)

iTunes下载（32位）：[https://www.apple.com/itunes/download/win32](https://www.apple.com/itunes/download/win32)

iCloud下载：[https://updates.cdn-apple.com/2020/windows/001-39935-20200911-1A70AA56-F448-11EA-8CC0-99D41950005E/iCloudSetup.exe](https://updates.cdn-apple.com/2020/windows/001-39935-20200911-1A70AA56-F448-11EA-8CC0-99D41950005E/iCloudSetup.exe)

然后对话框就消失了。对没错，就消失了。千万不要手贱去疯狂的点开始菜单里的AltServer，否则就会这样：

![一堆AltServer的图标堆在一起。](图6.webp)

是的没错，这玩意运行之后只会在任务栏的托盘里显示一个logo！现在，连接好你的设备，左键（记得是左键！点右键是没反应的）点一下这个logo，在弹出的窗口里选择“Install AltStore”>你的设备名。

![AltServer菜单。](图7.webp)

然后会提示输入账号密码，这里输入真实的密码即可。有的老教程会提到App专用密码，现在并不需要创建什么App专用密码，就算开启了双重认证也没有关系。

![AltServer输入账号密码。](图8.webp)

等待一段时间，就可以看到手机上出现了AltStore的logo，点击运行。这时会提示“未受信任的开发者”，根据提示前往设置按一下“信任”。这时候就可以打开应用了，此时还需要输入一遍账号和密码，必须和电脑端操作时的账号一样，不然会出问题。

\[info\]自从iOS 16后，苹果对开发者应用做出了一点点的限制，需要到手机的“设置”>“隐私与安全性”>“开发者模式”里把开发者模式打开。这个选项只有iPhone才有，iPad不需要这一步。\[/info\]

然后就可以愉快的操作了，找到“My Apps”选项卡，点一下左上角的“+”就可以安装应用了。

![AltStore操作界面。](图9.webp)

就是左上角那个”+“，另外，记得要先把安装包传到手机上。

这个过程中全程都需要连接电脑。AltStore官方推荐打开iTunes中“通过Wi-Fi与此设备同步”，不过实际操作下来发现体验不算特别好，电脑关机之后就无法自动连接设备了，还是要先插一次线激活连接。

![iTunes配置无线同步。](图10.webp)

先打开你的设备，然后直接往下滚动就可以找到这个设置

\[info\]

在[iOS侧载：引入]里提到过，如果是免费开发者，那么只能在一台设备上安装三个软件。AltStore可以自动处理这个事情，如果你需要安装三个以上应用，那么AltStore会先提醒你“Deactivate（禁用）”一款软件。

如果你的设备比较新，但又不是那么新，那么是可以绕开这个限制的，请继续往下看。

另外，还有一个硬性限制是10个“App ID”的限制。正常来讲，AltStore会用掉两个ID，剩下的软件都会用掉一个ID。这个限制是在云端处理的，所以无法绕开。

\[/info\]

## macOS食用方法

Mac的操作方法相对简单，因为不存在驱动的问题。（要是Mac连接不了iPhone那真是闹鬼了?）

\[info\]因为我没有合适的Mac，所以下面压根没有截图（还是那句话，那你写个der的教程啊！）\[/info\]

\[warning\]AltServer只支持Mac OS X 10.14.4及以上版本，其他版本无法使用。\[/warning\]

首先还是一样，下载AltServer本体，然后像正常安装软件一样把AltServer拖进Applications文件夹里。

然后运行AltServer，跟在Windows上一样，只会在任务栏里显示一个图标。

同样连接好设备，选择“Install AltStore”>你的设备名。这时会弹出要求安装一个邮件插件，按照指示前往“邮件”App安装并启用插件即可。（也就是利用这个插件替代了账号密码的身份验证过程。）

\[info\]启用插件的方法：“邮件”>“通用”>“管理插件”。\[/info\]

然后再次前往AltServer安装AltStore，剩下的过程和Windows一模一样。

## 绕开3个App限制的方法

在iOS 14.0 – 16.1.2（除了15.7.2）有一个漏洞（俗称bug，啊不对，特性?），被称为MacDirtyCow。

\[info\]iOS 16.2以及更新的版本修复了这个漏洞，不要有侥幸心理。\[/info\]

有大神在此基础上开发了一个软件，可以在[GitHub](https://github.com/zhuowei/WDBRemoveThreeAppLimit/releases)上下载。（还是那句话，下不下来多试几次，或者科学上网）

会下载下来一个.ipa格式的安装包，用AltStore把这个软件侧载上去。

\[info\]MacDirtyCow是一个漏洞，因此下载下来的文件可能会被报毒。如果被杀毒软件报毒，请添加信任后在下载一次。\[/info\]

\[info\]虽然官网的教程写的是iOS 14.0 – 16.1.2，不过这个软件并不支持iOS 14.x。所以又一次没有截图?\[/info\]

安装好这个软件后，点一下上面的“Go”。然后回到AltStore，找到“Settings”选项卡，先滚动到最底部，然后向上划三次。这时会多出一个选项，叫“Enforce 3 Apps Limit”。如果需要绕开限制，把这个选项关闭即可。

\[warning\]依然存在10个App ID的限制，在上面的教程中已经提到过。\[/warning\]


