---
title: Miniconda的安装和使用
date: 2025-03-02 16:52:35
tags: [conda]
categories: [conda,Python]
---

# Miniconda的安装和使用

> ## Excerpt
> 参考文献 Miniconda Anaconda 简介 Miniconda和Anaconda都是Python环境管理工具，可以用于创建、管理和部署Python环境及其依赖的软件包。它们的主要区别在于其默认安装的软件包和所需空间的大小。 Miniconda 是一个轻量级的Python环境管理工具，仅包括

---
> **参考文献**
> 
> [Miniconda](https://docs.conda.io/en/latest/miniconda.html) [Anaconda](https://www.anaconda.com/)

## 简介[#](https://www.cnblogs.com/jijunhao/p/17235904.html#%E7%AE%80%E4%BB%8B)

`Miniconda`和`Anaconda`都是Python环境管理工具，可以用于创建、管理和部署Python环境及其依赖的软件包。它们的主要区别在于其默认安装的软件包和所需空间的大小。

-   Miniconda 是一个轻量级的Python环境管理工具，仅包括conda、Python及其所需的基本依赖库。因此，它的安装包大小较小，只有几十兆，相比于Anaconda更加灵活。用户可以根据自己的需要逐步安装所需的软件包，避免不必要的浪费。在需要安装新软件包时，可以使用conda install命令来安装所需的软件包。这使得Miniconda在轻量化、快速安装、定制化、跨平台方面具有优势。
    
-   Anaconda 是一个包含了数百个预安装软件包的Python环境管理工具，包括Python解释器、各种科学计算和数据分析库、可视化工具、深度学习框架等。Anaconda旨在为数据科学家和研究者提供一个完整的数据科学环境，可以直接安装并使用大量的数据科学工具。这也意味着，Anaconda的安装包非常大，通常需要几个GB的磁盘空间，安装所需的时间也较长。同时，由于默认安装了大量的软件包，如果不需要的话，可能会浪费磁盘空间和内存资源。
    

综上所述，如果您需要一个灵活、快速、定制化的Python环境管理工具，并且希望自己安装所需的软件包，那么Miniconda可能更适合您。如果您需要一个预装有大量数据科学工具的环境，那么Anaconda可能更适合您。两者安装步骤几乎一致。

## 1\. 安装 Miniconda[#](https://www.cnblogs.com/jijunhao/p/17235904.html#1-%E5%AE%89%E8%A3%85-miniconda)

### 1.1 Windows下安装[#](https://www.cnblogs.com/jijunhao/p/17235904.html#11-windows%E4%B8%8B%E5%AE%89%E8%A3%85)

在 Windows 系统下安装 Miniconda，可以按照以下步骤进行：

-   首先，从官网下载适合你 Windows 系统的 Miniconda 安装程序：[https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)
    
-   下载完成后，双击安装程序并按照提示进行安装。
    
-   安装过程中需要阅读并同意许可协议。
    
-   安装过程中需要选择 Miniconda 的安装路径。默认情况下是在 `C:\Users\<username>\Miniconda3` 目录下创建一个名为 `Miniconda3` 的目录。你也可以选择其他路径，根据提示进行选择。
    

安装完成后，你就可以在终端中使用 conda 命令了，创建环境，安装依赖等操作都可以使用 conda 命令完成。

### 1.2 macOS下安装[#](https://www.cnblogs.com/jijunhao/p/17235904.html#12-macos%E4%B8%8B%E5%AE%89%E8%A3%85)

在 macOS 系统下安装 Miniconda，可以按照以下步骤进行：

-   首先，从官网下载适合你 macOS 系统的 Miniconda 安装程序：[https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)
    
-   下载完成后，双击安装程序并按照提示进行安装。
    
-   安装过程中需要阅读并同意许可协议。
    
-   安装过程中需要选择 Miniconda 的安装路径。默认情况下是在用户目录下创建一个名为 `miniconda3` 的目录。你也可以选择其他路径，根据提示进行选择。
    
-   安装完成后，需要在终端中运行以下命令，以便 Miniconda 的环境变量生效：
    

```shell
source ~/.bash_profile
```

安装完成后，你就可以在终端中使用 conda 命令了，创建环境，安装依赖等操作都可以使用 conda 命令完成。

### 1.3 Linux下安装[#](https://www.cnblogs.com/jijunhao/p/17235904.html#13-linux%E4%B8%8B%E5%AE%89%E8%A3%85)

在 Linux 下安装 Miniconda，可以按照以下步骤进行：

-   首先，从官网下载适合你 Linux 系统的 Miniconda 安装程序：[https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)
    
-   打开终端，进入下载目录，执行以下命令，安装 Miniconda：
    

```shell
bash Miniconda3-latest-Linux-x86_64.sh
```

> **注意**：如果你下载的是不同版本的安装程序，文件名也会有所不同，请根据你下载的版本自行更改文件名。

-   执行安装命令后，会出现 Miniconda 许可协议的信息，按照提示阅读并同意协议，即输入`accept`
    
-   接下来会提示你选择安装路径，默认情况下是在用户目录下创建一个名为 `miniconda3` 的目录。你也可以选择其他路径，根据提示进行选择。
    
-   安装完成后，终端中会出现提示，说明 Miniconda 已经安装成功。需要重新打开终端，以便 Miniconda 的环境变量生效。
    

安装完成后，你就可以在终端中使用 conda 命令了，创建环境，安装依赖等操作都可以使用 conda 命令完成。

## 2\. 配置 Miniconda[#](https://www.cnblogs.com/jijunhao/p/17235904.html#2-%E9%85%8D%E7%BD%AE-miniconda)

-   打开终端或 Anaconda Prompt（Windows 用户）。
    
-   创建并激活 conda 环境：
    

```shell
conda create --name env_name conda activate env_name
```

这里的 `env_name` 是你想要创建的环境名称。

-   安装所需的包和工具：

```shell
conda install package_name
```

这里的 package\_name 是你想要安装的包名称。

-   可以通过修改 .condarc 文件来修改默认的 conda 配置。

> conda 配置文件的路径:
> 
> -   Linux/macOS: `~/.condarc` 或 `$HOME/.condarc`
>     
> -   Windows: `USERPROFILE%.condarc` 或 `C:\Users\username.condarc`
>     
> 
> 其中，`%USERPROFILE%` 为 Windows 系统环境变量，表示当前用户的主目录路径，`username` 为当前用户名。

## 3\. 常用的 conda 命令[#](https://www.cnblogs.com/jijunhao/p/17235904.html#3-%E5%B8%B8%E7%94%A8%E7%9A%84-conda-%E5%91%BD%E4%BB%A4)

conda 是一个用于包管理和环境管理的工具，可以方便地创建、安装、升级和删除不同的软件包和其依赖项。以下是一些常用的 conda 命令：

-   创建一个新的环境：

```shell
conda create --name env_name
```

`env_name` 为你想要创建的环境名称。

-   激活一个环境：

```shell
conda activate env_name
```

`env_name` 为你想要激活的环境名称。

-   在激活的环境中安装一个软件包：

```shell
conda install package_name
```

`package_name` 为你想要安装的软件包名称。

-   列出当前环境中安装的所有软件包：

```shell
conda list
```

-   列出所有可用的环境：

```shell
conda env list
```

-   更新 conda：

```shell
conda update conda
```

-   更新所有已安装的软件包：

```shell
conda update --all
```

-   从环境中删除一个软件包：

```shell
conda remove package_name
```

`package_name` 为你想要删除的软件包名称。

> 在使用conda创建虚拟环境时，默认会将虚拟环境的文件夹放在Anaconda/Miniconda的安装路径下的envs文件夹中，具体路径为：
> 
> -   Windows系统下：C:\\Anaconda3\\envs 或 C:\\Users\\你的用户名\\Anaconda3\\envs
> -   Linux/Mac系统下：/home/你的用户名/anaconda3/envs 或 /Users/你的用户名/anaconda3/envs

当然，你也可以使用conda config命令更改默认路径，例如：

```shell
conda config --add envs_dirs /path/to/new/envs/folder
```

这个命令会在新路径下创建一个名为envs的文件夹，用来存储所有的虚拟环境。

## 4\. conda 换源[#](https://www.cnblogs.com/jijunhao/p/17235904.html#4-conda-%E6%8D%A2%E6%BA%90)

如果你在使用 conda 时遇到网络问题，可以将 conda 的源换成清华源（[https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/）。具体步骤如下：](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/%EF%BC%89%E3%80%82%E5%85%B7%E4%BD%93%E6%AD%A5%E9%AA%A4%E5%A6%82%E4%B8%8B%EF%BC%9A)

-   打开终端或 Anaconda Prompt。
    
-   在命令提示符中输入以下命令：
    

```shell
conda config --show # 显示当前 conda 配置 conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ # 添加清华源的免费仓库 conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/ # 添加清华源的主要仓库 conda config --set show_channel_urls yes # 显示添加的所有仓库地址
```

这会将清华源添加到你的 conda 配置文件中。

-   执行 `conda update conda` 命令，以确保你的 conda 版本是最新的。
    
-   如果你要创建新的环境或安装新的软件包，请使用以下命令：
    

```shell
conda create --name env_name package_name
```

`env_name` 为你想要创建的环境名称，`package_name` 为你想要安装的软件包名称。

> 例如：`conda create -n pytorch python==3.8` 创建一个 pytorch 环境，pythoon 版本为3.8

-   如果你需要取消这些换源更改，可以使用以下命令：

```shell
conda config --remove-key channels # 移除添加的仓库地址 conda config --set show_channel_urls no # 不再显示仓库地址
```

除了清华源之外，还有不少其他的 conda 镜像源可以使用。以下是一些常用的 conda 镜像源及其地址：

-   中科大镜像源：[https://mirrors.ustc.edu.cn/anaconda/pkgs/main/](https://mirrors.ustc.edu.cn/anaconda/pkgs/main/)
-   阿里云镜像源：[https://mirrors.aliyun.com/anaconda/pkgs/main/](https://mirrors.aliyun.com/anaconda/pkgs/main/)
-   华为云镜像源：[https://mirrors.huaweicloud.com/repository/anaconda/pkgs/main/](https://mirrors.huaweicloud.com/repository/anaconda/pkgs/main/)
-   中国科学院开源协会镜像源：[https://mirrors.opencas.cn/anaconda/pkgs/main/](https://mirrors.opencas.cn/anaconda/pkgs/main/)
-   豆瓣镜像源：[https://pypi.douban.com/simple](https://pypi.douban.com/simple)

如果你想切换到其他镜像源，可以使用类似于切换清华源的方法，将需要的镜像源地址添加到 conda 配置文件中。

> 需要注意的是，不同的镜像源可能会有不同的速度和可靠性，建议根据自己的网络情况选择合适的镜像源。

## 5\. 总结[#](https://www.cnblogs.com/jijunhao/p/17235904.html#5-%E6%80%BB%E7%BB%93)

使用 conda 时，需要注意以下几点：

1.  **环境隔离**：conda 可以创建虚拟环境来隔离不同的 Python 包和版本。在使用 conda 安装包时，需要确保安装在正确的环境中，以免出现冲突或版本不兼容的问题。可以使用 `conda env list` 查看当前存在的环境，使用 `conda activate env_name` 激活指定的环境。
2.  **版本管理**：conda 可以安装不同版本的 Python 包和库，并且可以轻松地切换不同版本之间。在安装新包或更新已有包时，需要注意是否与当前环境中的其他包兼容。可以使用 `conda search package_name` 命令查询指定包的可用版本，使用 `conda install package_name=version` 命令安装指定版本的包。
3.  **包管理**：conda 不仅可以安装 Python 包和库，还可以安装其他语言的依赖库和系统工具。在使用 conda 安装包时，需要注意包的来源和可靠性，以免下载和安装恶意软件。可以使用官方的 conda-forge 渠道来安装社区维护的包，也可以使用其他可信的镜像源。
4.  **配置管理**：conda 可以通过配置文件来管理镜像源、默认安装路径、自动激活环境等设置。在使用 conda 时，需要注意配置文件是否正确，以免出现安装失败或异常的问题。可以使用 `conda config --show` 命令查看当前的配置信息，使用 `conda config --set key=value` 命令修改指定的配置项。

总之，在使用 conda 时，需要仔细阅读文档，遵循最佳实践，以免出现不必要的问题。以上就是一些常用的 conda 小技巧。
