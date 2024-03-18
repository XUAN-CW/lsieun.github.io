---
title: "CentOS6.8"
sequence: "centos-iso"
---

## 1、下载地址 ##

下载地址：http://vault.centos.org/6.8/isos/x86_64/

问题：我没有下载成功唉！！！

{:refdef: style="text-align: center;"}
![](/assets/images/linux/concept/centos6.8-download.png)
{:refdef}

## 2、CentOS LiveCD、LiveDVD和BinDVD区别在哪里？ ##

在Centos官方选择下载CentOS的时候有好几个文件可供下载，包括liveCD、liveDVD和bin-DVD等等。这些文件都有什么区别，我们应该选择哪个文件下载呢？

- **liveDVD版本**：它就是一个体验版，无需安装到硬盘，插入光盘就可以通过光盘软件并体验CentOS的各种功能。可通过liveDVD启动电脑，启动出CentOS系统，也有图形界面，也有终端，也可以安装到计算机，但是有些内容可能还需要再次到网站下载（自动）。
- **liveCD版本**：和liveDVD一样，也是一个体验版和DVD体验版唯一的区别就是CD的存储空间要小一些，文件也会小一些，里面的软件包少一点。
- **bin-DVD版本**：这个版本就是普通的安装版本（即需要安装到计算机硬盘才能用）。这个版本的文件很大，时里包含了大量的常用软件，这样安装系统时候就可以直接安装而无需从网络上再去下载了。如果需要给服务器安装一个centos系统到硬盘，就需要选择这个版本。
- **minimal版本**：和bin-DVD一样它也是一个安装版镜像文件，只是minimal这个文件中只包含了系统和系统必须的几个基本软件包。
- **netinstall版本**：和bin-DVD一样它也是一个安装版镜像文件，但是netinstall的软件包都需要通过网络下载进行安装，而bin-DVD镜像自身包含了离线的软件包无需下载。

总结：

- （1）live表示无需安装到硬盘，就能直接在CD或DVD上直接运行。
- （2）CD与DVD的区别就是，CD的容易要小。
- （3）LiveCD 是可以直接在光盘上运行的版本，运行后可以再选择安装到硬盘中。
- （4）bin-DVD 是一个纯安装版本，一般推荐用这个。因为 LiveCD 安装的时候很多软件包要从网络去下载，会很慢。

## 3、CentOS系统BinDVD镜像为什么有两个呢？ ##

CentOS系统BinDVD镜像有两个。安装系统时，只用到第一个镜像就可以，即CentOS-6.x-i386-bin-DVD1.iso(32位)或者CentOS-6.x-x86_64-bin-DVD1.iso(64位)；而第二个镜像是系统自带软件安装包。 
