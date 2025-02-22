---
title: 【APP 逆向百例】某瓣 app 逆向分析
date: 2025-02-21 11:04:06
categories:
- 爬虫
tags:
- 爬虫
- 豆瓣
---

# 【APP 逆向百例】某瓣 app 逆向分析 - K哥爬虫 - 博客园

> ## Excerpt
> 某瓣 app 逆向分析 声明 本文章中所有内容仅供学习交流使用，不用于其他任何目的，不提供完整代码，抓包内容、敏感网址、数据接口等均已做脱敏处理，严禁用于商业用途和非法用途，否则由此产生的一切后果均与作者无关！ 本文章未经许可禁止转载，禁止任何修改后二次传播，擅自使用本文讲解的技术而导致的任何意外，

---
## 某瓣 app 逆向分析

## 声明[#](https://www.cnblogs.com/ikdl/p/18668799#%E5%A3%B0%E6%98%8E)

**本文章中所有内容仅供学习交流使用，不用于其他任何目的，不提供完整代码，抓包内容、敏感网址、数据接口等均已做脱敏处理，严禁用于商业用途和非法用途，否则由此产生的一切后果均与作者无关！**

**本文章未经许可禁止转载，禁止任何修改后二次传播，擅自使用本文讲解的技术而导致的任何意外，作者均不负责，若有侵权，请在公众号【K哥爬虫】联系作者立即删除！**

## 逆向目标[#](https://www.cnblogs.com/ikdl/p/18668799#%E9%80%86%E5%90%91%E7%9B%AE%E6%A0%87)

-   目标：某瓣 APP
-   apk 版本：7.89
-   逆向参数：\_sig 参数
-   下载地址：aHR0cHM6Ly93d3cud2FuZG91amlhLmNvbS9hcHBzLzYyMjg0NDc=

作为 k 哥第一篇 APP 逆向文章，我们先简单了解一些常见工具：

**SDK Platform-Tools** 是 Android 开发工具的一部分，由 Google 提供，主要用于与 Android 设备交互。它是开发者调试、管理设备以及支持应用程序开发的核心工具包，通常作为 Android SDK 的一部分使用。

## 下载地址[#](https://www.cnblogs.com/ikdl/p/18668799#%E4%B8%8B%E8%BD%BD%E5%9C%B0%E5%9D%80)

[AndroidDevTools - Android开发工具](https://www.androiddevtools.cn/)

[![7VKjGY.png](7VKjGY.png)](https://v1.ax1x.com/2024/12/24/7VKjGY.png)

## 工具简介[#](https://www.cnblogs.com/ikdl/p/18668799#%E5%B7%A5%E5%85%B7%E7%AE%80%E4%BB%8B)

### 常见工具[#](https://www.cnblogs.com/ikdl/p/18668799#%E5%B8%B8%E8%A7%81%E5%B7%A5%E5%85%B7)

SDK Platform-Tools 包含多个实用工具，其中最常用的是 **ADB（Android Debug Bridge）**。

#### 什么是 ADB？[#](https://www.cnblogs.com/ikdl/p/18668799#%E4%BB%80%E4%B9%88%E6%98%AF-adb)

ADB 是一个通用的命令行工具，提供 Android 设备与 PC 端之间的桥梁。通过 ADB，用户可以：

-   安装和调试应用程序。
-   操作设备上的文件。
-   查看设备的状态信息。
-   执行其他与设备相关的操作。

#### 安装 Platform-Tools[#](https://www.cnblogs.com/ikdl/p/18668799#%E5%AE%89%E8%A3%85-platform-tools)

1.  下载对应平台的 SDK Platform-Tools（Windows/Mac/Linux）。
2.  解压文件到本地目录，例如 `D:\platform-tools`。
3.  配置环境变量：
    -   将解压目录添加到系统的 PATH 环境变量中，以便在任意位置使用 ADB 命令。

___

## ADB 的基本用法[#](https://www.cnblogs.com/ikdl/p/18668799#adb-%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95)

以下是常用的 ADB 命令及其功能：

### 1\. 查看已连接设备[#](https://www.cnblogs.com/ikdl/p/18668799#1-%E6%9F%A5%E7%9C%8B%E5%B7%B2%E8%BF%9E%E6%8E%A5%E8%AE%BE%E5%A4%87)

```undefined
adb devices
```

输出示例：

```ruby
List of devices attached 1234567890abcdef device
```

### 2\. 安装 APK 文件[#](https://www.cnblogs.com/ikdl/p/18668799#2-%E5%AE%89%E8%A3%85-apk-%E6%96%87%E4%BB%B6)

```xml
adb install <apk_file_path>
```

示例：

```mipsasm
adb install my_app.apk
```

### 3\. 卸载应用[#](https://www.cnblogs.com/ikdl/p/18668799#3-%E5%8D%B8%E8%BD%BD%E5%BA%94%E7%94%A8)

```xml
adb uninstall <package_name>
```

示例：

```avrasm
adb uninstall com.example.myapp
```

### 4\. 推送文件到设备[#](https://www.cnblogs.com/ikdl/p/18668799#4-%E6%8E%A8%E9%80%81%E6%96%87%E4%BB%B6%E5%88%B0%E8%AE%BE%E5%A4%87)

```xml
adb push <local_file> <remote_path>
```

示例：

```bash
adb push my_file.txt /sdcard/
```

### 5\. 从设备拉取文件[#](https://www.cnblogs.com/ikdl/p/18668799#5-%E4%BB%8E%E8%AE%BE%E5%A4%87%E6%8B%89%E5%8F%96%E6%96%87%E4%BB%B6)

```xml
adb pull <remote_file> <local_path>
```

示例：

```bash
adb pull /sdcard/my_file.txt ./local_copy.txt
```

### 6\. 进入设备的 shell[#](https://www.cnblogs.com/ikdl/p/18668799#6-%E8%BF%9B%E5%85%A5%E8%AE%BE%E5%A4%87%E7%9A%84-shell)

```mipsasm
adb shell
```

进入 shell 后，可以执行设备上的 Linux 命令，例如：

```bash
ls /sdcard/
```

### 7\. 重启设备[#](https://www.cnblogs.com/ikdl/p/18668799#7-%E9%87%8D%E5%90%AF%E8%AE%BE%E5%A4%87)

```undefined
adb reboot
```

## jadx[#](https://www.cnblogs.com/ikdl/p/18668799#jadx)

**Jadx** 是一款开源的反编译工具，主要用于将 Android 应用程序的 APK 文件或 DEX 文件反编译为人类可读的 Java 源代码或 Smali 代码。它支持图形界面操作，是 Android 逆向工程中常用的工具之一。

___

## 下载地址[#](https://www.cnblogs.com/ikdl/p/18668799#%E4%B8%8B%E8%BD%BD%E5%9C%B0%E5%9D%80-1)

[Jadx Releases (v1.5.1)](https://github.com/skylot/jadx/releases/tag/v1.5.1)

[![7VKnzH.png](7VKnzH.png)](https://v1.ax1x.com/2024/12/24/7VKnzH.png)

## 安装和运行[#](https://www.cnblogs.com/ikdl/p/18668799#%E5%AE%89%E8%A3%85%E5%92%8C%E8%BF%90%E8%A1%8C)

### 1\. 下载并解压[#](https://www.cnblogs.com/ikdl/p/18668799#1-%E4%B8%8B%E8%BD%BD%E5%B9%B6%E8%A7%A3%E5%8E%8B)

1.  从[下载地址](https://github.com/skylot/jadx/releases/tag/v1.5.1)获取工具包。
2.  解压到本地目录，例如：`jadx/`。

### 2\. 启动 Jadx[#](https://www.cnblogs.com/ikdl/p/18668799#2-%E5%90%AF%E5%8A%A8-jadx)

双击运行 **`jadx-gui`** 文件，启动图形界面。

### 3.加载APK 文件[#](https://www.cnblogs.com/ikdl/p/18668799#3%E5%8A%A0%E8%BD%BDapk-%E6%96%87%E4%BB%B6)

使用图形界面载入 APK 文件，工具会自动将 APK 中的 DEX 文件解码并展示为 Java 源代码。

1.  打开 Jadx 图形界面。
2.  点击 **File -> Open File**，选择需要分析的 APK 文件。
3.  等待加载完成后，浏览解码后的 Java 源代码。

## frida[#](https://www.cnblogs.com/ikdl/p/18668799#frida)

Frida 是一款轻量级的 Hook 框架，也是一种动态插桩工具，可以插入代码到原生应用的内存空间，从而动态监视和修改其行为。Frida 支持多个平台，包括 Windows、Mac、Linux、Android 和 iOS。

### Frida 的组成[#](https://www.cnblogs.com/ikdl/p/18668799#frida-%E7%9A%84%E7%BB%84%E6%88%90)

Frida 分为两部分：

1.  **服务端**：运行在目标机器上，通过进程注入劫持应用的类和函数。
2.  **客户端**：运行在自己的设备上，用于注入自定义脚本（支持 JavaScript、Python、C 等）。

### 环境准备[#](https://www.cnblogs.com/ikdl/p/18668799#%E7%8E%AF%E5%A2%83%E5%87%86%E5%A4%87)

需要安装以下内容：

-   **Frida Server**：运行在目标设备上。
-   **Frida Tools**：运行在本地，用于与服务端交互。

以下以 **Frida 16.5.6** 和 **Android ARM64** 系统为例。

___

### 安装 Frida Server[#](https://www.cnblogs.com/ikdl/p/18668799#%E5%AE%89%E8%A3%85-frida-server)

Frida Server 有两个版本：

1.  **普通版**：[Releases · frida/frida](https://github.com/frida/frida/releases)
2.  **魔改版**（防检测优化版）：[Releases · hzzheyang/strongR-frida-android](https://github.com/hzzheyang/strongR-frida-android/releases)

#### 下载并安装 Frida Server[#](https://www.cnblogs.com/ikdl/p/18668799#%E4%B8%8B%E8%BD%BD%E5%B9%B6%E5%AE%89%E8%A3%85-frida-server)

1.  下载对应版本的 Frida Server 文件：
    
    -   选择普通版或魔改版。
    -   确保下载与目标设备架构匹配的版本（如 ARM64）。
2.  使用 ADB 命令将文件传输到目标设备：
    
    ```bash
    adb push frida-server-16.5.6-android-arm64 /data/local/tmp/
    ```
    
3.  （可选）传输魔改版文件，命令类似，此处不再赘述。
    
4.  修改 Frida Server 的权限并启动服务：
    
    ```kotlin
    adb shell // 进入手机 su // 切换成root cd /data/local/tmp/ // 进入 tmp 文件 chmod 777 frida-server-16.5.6-android-arm64 //修改文件权限 ./frida-server-16.5.6-android-arm64 启动 frida 服务端
    ```
    

___

### 安装 Frida Client[#](https://www.cnblogs.com/ikdl/p/18668799#%E5%AE%89%E8%A3%85-frida-client)

在本地使用 pip 安装 Frida Client 和 Frida Tools：

```bash
pip install frida==16.5.6 pip install frida-tools==13.6.0
```

安装完成后，可使用以下命令验证安装：

```bash
frida --version
```

___

### Frida 的基本用法[#](https://www.cnblogs.com/ikdl/p/18668799#frida-%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95)

Frida 的基本用法主要有两种形式：

#### 1\. 附加到正在运行的应用[#](https://www.cnblogs.com/ikdl/p/18668799#1-%E9%99%84%E5%8A%A0%E5%88%B0%E6%AD%A3%E5%9C%A8%E8%BF%90%E8%A1%8C%E7%9A%84%E5%BA%94%E7%94%A8)

使用 `-U` 和 `-F` 参数附加到设备上正在运行的应用程序：

```bash
frida -U -F -l script.js
```

-   `-U`：通过 USB 连接的设备。
-   `-F`：附加到设备上当前正在运行的应用（无需手动指定包名）。
-   `-l script.js`：运行指定的 JavaScript 脚本（如 `script.js`）。

#### 2\. 强制启动并附加到指定应用[#](https://www.cnblogs.com/ikdl/p/18668799#2-%E5%BC%BA%E5%88%B6%E5%90%AF%E5%8A%A8%E5%B9%B6%E9%99%84%E5%8A%A0%E5%88%B0%E6%8C%87%E5%AE%9A%E5%BA%94%E7%94%A8)

使用 `-f` 参数强制启动并附加到指定的应用：

```javascript
frida -U -f com.package.name -l script.js
```

-   `-f`：强制启动应用。
-   `com.package.name`：目标应用的包名。
-   `-l script.js`：运行指定的 JavaScript 脚本。

## ida:[#](https://www.cnblogs.com/ikdl/p/18668799#ida)

**IDA**（Interactive Disassembler Professional）是一款功能强大的交互式静态反汇编工具，广泛应用于程序分析和逆向工程。它具有以下特点：

-   **多处理器支持**：支持多种架构的二进制文件分析。
-   **跨平台**：支持 Windows、Linux、MacOS 等平台的程序分析。
-   **可编程和可扩展**：通过 Python 或 IDC 脚本扩展功能。
-   **交互式操作**：用户可以在反汇编的基础上动态修改和注释。

___

## IDA 的下载和版本说明[#](https://www.cnblogs.com/ikdl/p/18668799#ida-%E7%9A%84%E4%B8%8B%E8%BD%BD%E5%92%8C%E7%89%88%E6%9C%AC%E8%AF%B4%E6%98%8E)

IDA 是一款商业工具，正版软件需要授权。如果只是学习使用，可以在社区论坛（如吾爱破解）找到适合的版本。注意不要用于非法用途。

___

## IDA 的常用快捷键[#](https://www.cnblogs.com/ikdl/p/18668799#ida-%E7%9A%84%E5%B8%B8%E7%94%A8%E5%BF%AB%E6%8D%B7%E9%94%AE)

这里简单介绍一下快捷键，帮助快速上手：

| 快捷键 | 功能说明 |
| --- | --- |
| **空格** | 在 **图形视图（Graph View）** 和 **汇编代码视图（Text View）** 之间切换。 |
| **F5** | 反编译代码，生成伪 C 代码（仅在支持的架构中可用）。 |
| **G** | 跳转到指定地址。 |
| **X** | 查看某个函数或变量的交叉引用（Xref）。 |
| **N** | 更改变量或函数的名称（命名更直观）。 |
| **Y** | 更改变量或函数的类型。 |
| **Ctrl + F** | 搜索字符串、代码或地址。 |
| **Alt + T** | 查找特定的函数、变量或模块（导航更快捷）。 |
| **Ctrl + Space** | 快速切换视图模式，便于分析。 |

生于某瓣，始于某瓣，在介绍了常用的逆向工具之后，我们可以开始我们的主题。

## 抓包分析[#](https://www.cnblogs.com/ikdl/p/18668799#%E6%8A%93%E5%8C%85%E5%88%86%E6%9E%90)

打开 `app`，在首页进行刷新，`charles` 配合 `SocksDroid` 进行抓包，结果如下：

[![7VKfHU.png](7VKfHU.png)](https://v1.ax1x.com/2024/12/24/7VKfHU.png)

其中要逆向的参数为 `_sig` 参数。

## 逆向分析[#](https://www.cnblogs.com/ikdl/p/18668799#%E9%80%86%E5%90%91%E5%88%86%E6%9E%90)

我们把 `apk` 文件拖到 `jadx` 进行分析：

直接搜索 `_sig` 参数，点进去：

[![7VKi1q.png](7VKi1q.png)](https://v1.ax1x.com/2024/12/24/7VKi1q.png)

[![7VKs2s.png](7VKs2s.png)](https://v1.ax1x.com/2024/12/24/7VKs2s.png)

```java
Pair F3 = i0.d.F(request); request = request.newBuilder() .url( request.url() .newBuilder() .setQueryParameter("_sig", (String) F3.first) .setQueryParameter(bs.h, (String) F3.second) .build() ) .build();
```

发现新增了以下两个查询参数参数值，其中就有我们的 `_sig` 参数，点进去F 方法：

[![7VK6Qa.png](7VK6Qa.png)](https://v1.ax1x.com/2024/12/24/7VK6Qa.png)

只是对 `header` 做了一些操作，点进去 E 方法：

[![7VKFv7.png](7VKFv7.png)](https://v1.ax1x.com/2024/12/24/7VKFv7.png)

这个 E 很有可能是我们参数的生成地方，我们右键 E 方法复制 `frida` 代码，`frida` 完整代码如下：

```javascript
function hook1(){ let d = Java.use("i0.d"); d["E"].implementation = function (str, str2, str3) { console.log('E is called' + ', ' + 'str: ' + str + ', ' + 'str2: ' + str2 + ', ' + 'str3: ' + str3); let ret = this.E(str, str2, str3); console.log('E ret value is ' + ret); return ret; }; } function main(){ Java.perform(function (){ hook1() }) } setImmediate(main)
```

使用如下 `frida` 命令启动发现 `frida` 退出，而我们 `APP` 没有退出，这说明我们 `frida` 被检测了：

```avrasm
frida -U -f com.douban.frodo -l 脚本名.js
```

[![7VKZnI.png](7VKZnI.png)](https://v1.ax1x.com/2024/12/24/7VKZnI.png)

我们可以先`hook dlopen` 方法，看看是打开了哪个 `so` 文件退出了，`dlopen` 是一个能动态加载指定的共享库到内存中，基本上所有的 `so` 文件加载都要经过该方法，`hook` 代码如下：

```javascript
var dlopen = Module.findExportByName(null, "dlopen"); var android_dlopen_ext = Module.findExportByName(null, "android_dlopen_ext"); Interceptor.attach(dlopen, { onEnter: function (args) { var path_ptr = args[0]; var path = ptr(path_ptr).readCString(); console.log("[dlopen -> enter", path); }, onLeave: function (retval) { console.log("dlopen -> leave") } }); Interceptor.attach(android_dlopen_ext, { onEnter: function (args) { var path_ptr = args[0]; var path = ptr(path_ptr).readCString(); console.log("[android_dlopen_ext -> enter", path); }, onLeave: function (retval) { console.log("android_dlopen_ext -> leave") } });
```

[![7VKeLV.png](7VKeLV.png)](https://v1.ax1x.com/2024/12/24/7VKeLV.png)

发现 `libmsaoaidsec.so` 并没有 `leave`，推测是在该 `so` 文件里面开启了线程，做循环检测，我们尝试 `hook pthread` 方法，`pthread` 用于线程的创建、同步、管理和终止，`hook` 代码如下：

```javascript
function hook_pth() { var pth_create = Module.findExportByName("libc.so", "pthread_create"); console.log("[pth_create]", pth_create); Interceptor.attach(pth_create, { onEnter: function (args) { var module = Process.findModuleByAddress(args[2]); if (module != null) { console.log("开启线程-->", module.name, args[2].sub(module.base)); } }, onLeave: function (retval) {} }); } hook_pth()
```

可以发现在这个so 文件开启了两个线程，地址分别是`0x1c544` 和 `0x1b8d4`：

[![7VKoxL.png](7VKoxL.png)](https://v1.ax1x.com/2024/12/24/7VKoxL.png)

我们可以把这个 `so` 文件，拿到 `ida` 分析，分别搜索这两个地址，看看都做了什么操作：

`0x1c544`：

[![7Vb9zJ.png](7Vb9zJ.png)](https://v1.ax1x.com/2024/12/24/7Vb9zJ.png)

[![7VbB9G.png](7VbB9G.png)](https://v1.ax1x.com/2024/12/24/7VbB9G.png)

代码很长，看着看着像是在检测一些字符的长度。

0x1b8d4：

[![7VbTKB.png](7VbTKB.png)](https://v1.ax1x.com/2024/12/24/7VbTKB.png)

这个函数一个死循环，并且有一个`usleep(v1)` 很可疑，像是在做循环检测。我们可以先把这个函数给替换掉,替换的时候要注意，有可能只 `hook` 这个地方可能不行，我们需要找到其他函数调用这个函数，也就是要找到他的引用，可以按住 x 看到函数的交叉引用。另外这个 `hook` 时机要早，因为这个函数的调用是通过 `init_proc` 调用的：

[![7Vbm1t.png](7Vbm1t.png)](https://v1.ax1x.com/2024/12/24/7Vbm1t.png)

我们可以通过hook `call_constructors` 这个， `call_constructors` 主要作用是执行那些需要在程序开始运行之前完成初始化的代码，hook 代码如下：

```javascript
function hook_call_constructors() { var linker64_base_addr = Module.getBaseAddress("linker64") var call_constructors_func_off = 0x4a174 var call_constructors_func_addr = linker64_base_addr.add(call_constructors_func_off) var listener = Interceptor.attach(call_constructors_func_addr, { onEnter: function (args) { console.log("call_constructors -> enter") var module = Process.findModuleByName("libmsaoaidsec.so") if (module != null) { Interceptor.replace(module.base.add(0x1B924), new NativeCallback(function () { console.log("替换成功") }, "void", [])) listener.detach() } }, }) }
```

通过打开这个 `libmsaoaidsec.so` 文件进行调用，完整代码如下：

```javascript
var dlopen = Module.findExportByName(null, "dlopen"); var android_dlopen_ext = Module.findExportByName(null, "android_dlopen_ext"); Interceptor.attach(dlopen, { onEnter: function (args) { var path_ptr = args[0]; var path = ptr(path_ptr).readCString(); console.log("[dlopen -> enter", path); }, onLeave: function (retval) { console.log("dlopen -> leave") } }); Interceptor.attach(android_dlopen_ext, { onEnter: function (args) { var path_ptr = args[0]; var path = ptr(path_ptr).readCString(); console.log("[android_dlopen_ext -> enter", path); if (args[0].readCString() != null && args[0].readCString().indexOf("libmsaoaidsec.so") >= 0) { hook_call_constructors() } }, onLeave: function (retval) { console.log("android_dlopen_ext -> leave") } }); function hook_call_constructors() { var linker64_base_addr = Module.getBaseAddress("linker64") var call_constructors_func_off = 0x4a174 var call_constructors_func_addr = linker64_base_addr.add(call_constructors_func_off) var listener = Interceptor.attach(call_constructors_func_addr, { onEnter: function (args) { console.log("call_constructors -> enter") var module = Process.findModuleByName("libmsaoaidsec.so") if (module != null) { Interceptor.replace(module.base.add(0x1B924), new NativeCallback(function () { console.log("替换成功") }, "void", [])) listener.detach() } }, }) }
```

最后成功过掉检测，接着继续hook 我们上面的 E 函数：

[![7Vbp6b.png](7Vbp6b.png)](https://v1.ax1x.com/2024/12/24/7Vbp6b.png)

[![7Vb0Qe.png](7Vb0Qe.png)](https://v1.ax1x.com/2024/12/24/7Vb0Qe.png)

发现结果一样，证明我们的位置没有找错，传入了三个参数分别为查询参数、请求方法 和 null:

```javascript
E is called, str: https://frodo.douban.com/api/v2/elendil/recommend_feed?start=0&count=20&screen_width=1080&screen_height=2028&wx_api_ver=0&opensdk_ver=638058496&webview_ua=Mozilla%2F5.0%20%28Linux%3B%20Android%2011%3B%20Pixel%203%20Build%2FRQ1D.210205.004%3B%20wv%29%20AppleWebKit%2F537.36%20%28KHTML%2C%20like%20Gecko%29%20Version%2F4.0%20Chrome%2F130.0.6723.107%20Mobile%20Safari%2F537.36&sugar=0&update_mark=1735024878.512534157&network=wifi&enable_sdk_bidding=1&apikey=0dad551ec0f84ed02907ff5c42e8ec70&channel=ali_market&udid=3e71b8653a2b6b25b07876b25012c50ae5074f2a&os_rom=android&oaid=EdGi3zYQCRzmwwB1YR7WKg%3D%3D%0A&timezone=Asia%2FShanghai, str2: GET, str3: null
```

[![7VblIw.png](7VblIw.png)](https://v1.ax1x.com/2024/12/24/7VblIw.png)

通过对传递的 `str` 参数不断操作，最终通过 `HMAC_SHA1` 算法生成加密值 `str4` 。其中算法的 key 值是由 `str5` 得来:

```java
String str5 = j7.e.d().f30170e.b;
```

点进该方法，可以发现算法 key 值是为 h 函数第三个参数的值：

[![7VbEL6.png](7VbEL6.png)](https://v1.ax1x.com/2024/12/24/7VbEL6.png)

直接 frida hook 该函数得到 `key` 值：

[![7VbQxO.png](7VbQxO.png)](https://v1.ax1x.com/2024/12/24/7VbQxO.png)

最终 python 代码如下:

```python
import hmac import hashlib import base64 def hmac_hash1(key: str, data: str) -> str: try: # 将 key 转换为字节 key_bytes = key.encode() # 将 data 转换为字节 data_bytes = data.encode() # 使用 HMAC-SHA1 进行加密 mac = hmac.new(key_bytes, data_bytes, hashlib.sha1) # 返回 Base64 编码的结果 return base64.b64encode(mac.digest()).decode('utf-8') except Exception as e: print(f"Error: {e}") return None if __name__ == '__main__': # 测试代码 key = "bf7dddc7c9cfe6f7" data = "GET&%2Fapi%2Fv2%2Felendil%2Frecommend_feed&1735019437" hashed_value = hmac_hash1(key, data) print("HMAC Hash (Base64):", hashed_value)
```

至此，该参数加密分析流程就结束了。

相关代码，会分享到知识星球当中，需要的小伙伴自取，仅供学习交流。

## 结果验证[#](https://www.cnblogs.com/ikdl/p/18668799#%E7%BB%93%E6%9E%9C%E9%AA%8C%E8%AF%81)