---
layout: post
title:  "Ubuntu 琐事"
date:   2021-10-27
categories: Linux
---

# Ubuntu 琐事


<!-- vim-markdown-toc GFM -->

* [Ubuntu分区管理-Ubuntu Partition](#ubuntu分区管理-ubuntu-partition)
    * [双系统卸载windows](#双系统卸载windows)
* [Ubuntu系统盘瘦身](#ubuntu系统盘瘦身)
    * [对于想要为系统盘瘦身的你的忠告](#对于想要为系统盘瘦身的你的忠告)
    * [清除apt缓存](#清除apt缓存)
    * [删除旧内核](#删除旧内核)
    * [删除孤立的库](#删除孤立的库)
    * [比较大的不常用Installed package](#比较大的不常用installed-package)
    * [管理包](#管理包)
    * [清除旧版本的snap applications](#清除旧版本的snap-applications)
    * [清除缩略图](#清除缩略图)
    * [清除残余配置文件](#清除残余配置文件)
    * [按需清理日志](#按需清理日志)
    * [更改apt-get下载地址](#更改apt-get下载地址)
    * [更改docker image存储路径](#更改docker-image存储路径)
* [打开缓存失败](#打开缓存失败)
* [perf安装的姿势](#perf安装的姿势)
* [dpkg处理软件包报错](#dpkg处理软件包报错)
* [Ubuntu源](#ubuntu源)
    * [改国内源](#改国内源)
    * [Hash Sum mismatch](#hash-sum-mismatch)
    * [GPG 错误](#gpg-错误)
* [Ubuntu亮度问题（16.04）](#ubuntu亮度问题1604)
* [.crx插件的安装](#crx插件的安装)
* [挂载硬盘的暗坑踩坑记录及正确姿势](#挂载硬盘的暗坑踩坑记录及正确姿势)
    * [挂载硬盘的正确姿势](#挂载硬盘的正确姿势)
* [代理姿势](#代理姿势)
    * [tty代理(环境变量)](#tty代理环境变量)
    * [apt-get代理](#apt-get代理)
    * [Git代理](#git代理)
    * [bp代理](#bp代理)
* [N卡独显大坑](#n卡独显大坑)
    * [显卡驱动自动安装/图形化界面更改显驱](#显卡驱动自动安装图形化界面更改显驱)
    * [更新bios后的显示不正常](#更新bios后的显示不正常)
    * [键盘延时？！](#键盘延时)
    * [xrandr报错 和 display resolution](#xrandr报错-和-display-resolution)
* [v2ray配置](#v2ray配置)
* [Appimage](#appimage)
    * [Cannot run due to existing symlinks in /tmp (FIXME)](#cannot-run-due-to-existing-symlinks-in-tmp-fixme)
    * [删除menu entries](#删除menu-entries)
* [Lua包管理，luarocks](#lua包管理luarocks)
* [burpsuite抓https包](#burpsuite抓https包)
* [ubuntu播放mp4](#ubuntu播放mp4)
* [vbox中虚拟机使用宿主机代理](#vbox中虚拟机使用宿主机代理)
* [Ubuntu安装jdk1.8及多jdk管理](#ubuntu安装jdk18及多jdk管理)
    * [ppa安装](#ppa安装)
    * [oracle官网安装](#oracle官网安装)
    * [安装openjdk-8-jdk](#安装openjdk-8-jdk)
    * [配置多版本](#配置多版本)
* [Java bug](#java-bug)
* [vmware](#vmware)
    * [无法reinstall vmware tools](#无法reinstall-vmware-tools)
* [Virtual Box](#virtual-box)
    * [多个vmdk合成一个](#多个vmdk合成一个)
    * [vbox failed to import appliance](#vbox-failed-to-import-appliance)
* [*e.g.The shopping channel is known for selling home appliances.*](#egthe-shopping-channel-is-known-for-selling-home-appliances)
        * [Image file corrupt](#image-file-corrupt)
        * [Attach as a virtual hard disk](#attach-as-a-virtual-hard-disk)
        * [Administrative privileges for vboxmanage.exe](#administrative-privileges-for-vboxmanageexe)
        * [Corrupted VirtualBox installation](#corrupted-virtualbox-installation)
* [vim](#vim)
    * [Ubuntu下的Markdown编辑器和markdown-toc](#ubuntu下的markdown编辑器和markdown-toc)
    * [Spacevim大坑](#spacevim大坑)
* [mega下载占盘太多](#mega下载占盘太多)
* [gnome](#gnome)
    * [Ubuntu gnome 美化](#ubuntu-gnome-美化)
    * [chrome安装gnome extension](#chrome安装gnome-extension)
    * [gnome录屏](#gnome录屏)
* [wine qq](#wine-qq)
    * [安装](#安装)
    * [wine-qq文件下载路径](#wine-qq文件下载路径)
* [娱乐](#娱乐)
    * [cmus](#cmus)
* [xampp](#xampp)
* [Install ROS on Ubuntu 20.04](#install-ros-on-ubuntu-2004)
    * [Use ROS's dependency management tool rosdep](#use-ross-dependency-management-tool-rosdep)
    * [Build catkin workspace](#build-catkin-workspace)
    * [Install ROS driver to communicate with parrot drones](#install-ros-driver-to-communicate-with-parrot-drones)

<!-- vim-markdown-toc -->

## Ubuntu分区管理-Ubuntu Partition

### 双系统卸载windows

网上说可以使用工具OS-Uninstaller直接完成
https://help.ubuntu.com/community/OS-Uninstaller
反正我失败了，被迫重装

## Ubuntu系统盘瘦身

### 对于想要为系统盘瘦身的你的忠告
**千万不要`apt autoremove`!!!!!**
**千万不要`apt autoremove`!!!!!**
**千万不要`apt autoremove`!!!!!**
只是一条堪称灾难的指令。如果不幸，它会把你的各种依赖删得七零八落，让你的系统变成灾难现场。--by 花了3h修复gcc的C_M.

### 清除apt缓存
对于不了解apt（repo）, ppa, dpkg的崽崽，请自己查看, 本部分不做详细说明.

查看apt的cache `sudo du -sh /var/cache/apt `
清除不必要的cache `sudo apt-get autoclean`
清除整个cache `sudo apt-get clean`

###  删除旧内核
`sudo dpkg --get-selections  | grep linux-image` 查看已安装内核映像
`uname -r`  查看当前内核版本
`sudo apt-get purge linux-image-2.6.32-26-generic` 删除旧的内核映像，只保留当前版本

`sudo dpkg --get-selections  | grep linux-headers`  查看已有的头文件库
`sudo apt-get purge linux-headers-2.6.28-19` 删除旧的头文件库
`sudo apt autoremove`

以上两步，对于权限不够的目录，在结束cd到上级目录，`sudo rm -rf XXX`

`dpkg --get-selections  | grep linux` 查看内核映像和组件
对于状态是`deinstall`的
`sudo dpkg -P linux-image-3.5.0-4[2-9]-generic `
完成

### 删除孤立的库
也挺危险的...
`sudo deborphan | xargs sudo apt-get -y remove --purge`

### 比较大的不常用Installed package
自己找找，删了就vans了。主要是安利下debian-goodies中的`dpigs`,方便啊:3

### 管理包
`sudo gtkorphan`

### 清除旧版本的snap applications
snap applications 一般比较大，可以清除其旧版本释放空间。

> Snappy is a software deployment and package management system developed by Canonical for the Linux operating system. The packages, called snaps, and the tool for using them, snapd, work across a range of Linux distributions allowing distribution-agnostic upstream software packaging. Snappy was originally designed for Ubuntu Touch. The system is designed to work for internet of things, cloud and desktop computing. --Wiki

查看占盘情况 `du -h /var/lib/snapd/snaps`

这里是Alan Pope (part of Snapcraft team at Canonical) 给出的shell脚本，清除旧版本

```bash
#!/bin/bash
# Removes old revisions of snaps
# CLOSE ALL SNAPS BEFORE RUNNING THIS
set -eu
snap list --all | awk '/disabled/{print $1, $3}' |
    while read snapname revision; do
        snap remove "$snapname" --revision="$revision"
    done
```
代码分析

 - set用来定制环境。-u,如果遇到不存在的变量，Bash 默认忽略它。-e脚本发生错误则终止执行。
 - awk在文件或者字符串中基于指定规则浏览和抽取信息. awk对输入的每一行，也就是`snap list --all`得到的之中/disabled/下的**每一行**（即旧版本的snap apps）. 输出第1个和第3个参数至stdout(**注意区分awk中$0是指整行,shell中的$0传的参是文件名**)。
 - $1这里是snapname, $3是revision. while循环,删除即可。


### 清除缩略图
查看缩略图缓存`du -sh ~/.cache/thumbnails`
清除`rm -rf ~/.cache/thumbnails/*`

> **关于du的说明**
> du用来查看文件大小
>  -h, --human-readable  以可读性较好的方式显示尺寸(例如：1K 234M 2G)
>  -s, --summarize       只分别计算命令列中每个参数所占的总用量
>  --max-depth=N     *显示目录总计(与--all 一起使用计算文件)*
>   *当N 为指定数值时计算深度为N；*
>   *--max-depth=0 等于--summarize*

### 清除残余配置文件
查看残余配置文件`dpkg --list | grep "^rc"`
rc表示软件包已经删除，配置文件还在.

提取这些软件包的名称`dpkg --list | grep "^rc" | cut -d " " -f 3`

删除这些软件包`dpkg --list | grep "^rc" | cut -d " " -f 3 | xargs sudo dpkg --purge`

### 按需清理日志
查看日志大小`du -h --max-depth=1 /var/log/*`

***对一些log的说明***

> /var/log/alternatives.log-更新替代信息都记录在这个文件中
> <br>/var/log/apport.log -应用程序崩溃记录
> <br>/var/log/apt/   -用apt-get安装卸载软件的信息
> <br>/var/log/auth.log  -登录认证log
> <br>/var/log/boot.log  -包含系统启动时的日志。 /var/log/btmp    -记录所有失败启动信息
> <br>/var/log/Consolekit  - 记录控制台信息
> <br>/var/log/cpus     - 涉及所有打印信息的日志
> <br>/var/log/dist-upgrade  - dist-upgrade这种更新方式的信息
> <br>/var/log/dmesg    -包含内核缓冲信息（kernel ringbuffer）。在系统启动时，显示屏幕上的与硬件有关的信息
> <br>/var/log/dpkg.log   - 包括安装或dpkg命令清除软件包的日志。
> <br>/var/log/faillog    - 包含用户登录失败信息。此外，错误登录命令也会记录在本文件中。
> <br>/var/log/fontconfig.log -与字体配置有关的log。
> <br>/var/log/fsck     - 文件系统日志
> <br>/var/log/faillog   -包含用户登录失败信息。此外，错误登录命令也会记录在本文件中。
> <br>/var/log/hp/
> <br>/var/log/install/
> <br>/var/log/jokey.log
> <br>/var/log/kern.log –包含内核产生的日志，有助于在定制内核时解决问题。
> <br>/var/log/lastlog —记录所有用户的最近信息。这不是一个ASCII文件，因此需要用lastlog命令查看内容。
> <br>/var/log/faillog –包含用户登录失败信息。此外，错误登录命令也会记录在本文件中。
> <br>/var/log/lightdm/
> <br>/var/log/mail/ – 这个子目录包含邮件服务器的额外日志。
> <br>/var/log/mail.err    -类似于上面的
> <br>/var/log/news/
> <br>/var/log/pm-powersave.log
> <br>/var/log/samba/ –包含由samba存储的信息。
> <br>/var/log/syss.log
> <br>/var/log/speech-dispacher/
> <br>/var/log/udev
> <br>/var/log/ufw.log
> <br>/var/log/upstart/
> <br>/var/log/uattended-upgrades/
> <br>/var/log/wtmp —包含登录信息。使用wtmp可以找出谁正在登陆进入系统，谁使用命令显示这个文件或信息等。
> <br>/var/log/xorg.*.log— 来自X的日志信息。

一般来说，公司的服务器之类的,syslog和kern.log比较大，可以这样清理
```
sudo -i
echo  > /var/log/syslog
echo  > /var/log/kern.log
```

对于PC，journalctl会比较大

> journalctl为什么这么大？因为全面～
> 在Systemd出现之前，Linux系统及各应用的日志都是分别管理的，Systemd开始统一管理了所有Unit的启动日志，这样带来的好处就是可以只用一个 journalctl命令，查看所有内核和应用的日志

这样来整理journal~
```
journalctl --disk-usage  //查看journal占用磁盘空间
journalctl --vacuum-size=500M //设置日志占用的空间
journalctl --vacuum-time=1month //设置日至保存时间，2d(就是2 days，按需设置参数即可)
```

### 更改apt-get下载地址
Ubuntu中使用apt-get install默认会把deb包下载到/var/cache/apt/archives/下，可以通过man apt-get来看到相应的设置
如何更改呢？
1 .在你想存放的位置建立一个文件夹
`mkdir -p /path/apt-archives`
2 .在/path/apt-archives/下建立一个partial文件夹
`mkdir partial`
3. 编辑/etc/apt/apt.conf，这个文件可能并不存在，直接vim就好，添加如下内容（记得用sudo）：
`dir::cache::archives /path/apt-archives;`

### 更改docker image存储路径
vbox太慢太卡，终于打算用docker了，但是有一点点问题，就是image太大了，如果全部存在`/var/lib/docker`下，系统盘很受伤。所以要更改存储路径
1.更改配置
```
mkdir /etc/systemd/system/docker.service.d
touch /etc/systemd/system/docker.service.d/docker-overlay.conf
vim /etc/systemd/system/docker.service.d/docker-overlay.conf
```
配置文件如下：
其中`/home/docker`是你将要存储的路径（建议在你挂载的非系统盘的硬盘下建一个）
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd --graph="/home/docker" --storage-driver=overlay
```
2.重启
```
sudo systemctl daemon-reload
sudo systemctl restart docker
```
3.查看是否更改成功
`sudo docker info`
注意看`Docker Root Dir:`这一项，这里就是你指定的位置

## 打开缓存失败

```bash
sudo rm /var/lib/apt/lists/* -vf
sudo apt-get update
```

## perf安装的姿势
（这个是真的坑，按照那种东缺点、西缺点的搞法，还定位不到缺的东西，难道要在网上下，然后一个个装吗？好像也未尝不是个办法呢~）
perf安装按网上的随便来会出向各种依赖问题，究其原因，是版本不对。解决方案也很简单，就是指定版本。   
首先`uname -r`查看
然后apt安装linux-tools时指定版本，也就是linux-tools-"你查到的版本"

## dpkg处理软件包报错
在<a>https://blog.csdn.net/u012483097/article/details/78994571</a>这里看到的解决方案
```
 sudo mv /var/lib/dpkg/info /var/lib/dpkg/info_old //现将info文件夹更名
sudo mkdir /var/lib/dpkg/info //再新建一个新的info文件夹
 sudo apt-get update && apt-get -f install //不用解释了吧
 sudo mv /var/lib/dpkg/info/* /var/lib/dpkg/info_old //新的info文件夹下生成的文件全部移到info_old文件夹下
 sudo rm -rf /var/lib/dpkg/info //把自己新建的info文件夹删掉
 sudo mv /var/lib/dpkg/info_old /var/lib/dpkg/info //把以前的info文件夹重新改
```

其实可以化简一下，先rm info,再创建，然后执行`sudo apt-get update && apt-get -f install`
这里-f是--fix-broken,是用来修复依赖关系的

## Ubuntu源
### 改国内源
`sudo vim /etc/apt/sources.list`

亦可用于多次配置报错问题的解决

### Hash Sum mismatch
用apt-get update更新源时，出现“Hash Sum mismatch”的报错
原因：透明缓存可以增加网络内部速度，减少出口的流量，但所获取的某些文件不是源服务器上的真正文件，是从缓存中获取的，当缓存中获取的一些校验信息跟源中不一致的时候，自然提示校验失败，无法继续更新。

清缓存法：
```
$ sudo apt-get clean  
$ sudo apt-get update --fix-missing
```

### GPG 错误

使用 `add-apt-repository`相当于是在source.list中添加了相关的源，并且会自动添加相应的key。若是直接在`source.list`中添加，则需要手动添加key.(也就是ppa源的网站上可以看到的fingerprint)

`sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys THE_KEY`

## Ubuntu亮度问题（16.04）
之前的brightness-controller在把py
1.`sudo apt-get install laptop-mode-tools`  
2.更改/etc/laptop-mode/laptop-mode.conf 文件：
`sudo gedit /etc/laptop-mode/laptop-mode.conf`
 令`ENABLE_LAPTOP_MODE_ON_AC=1`
3.更改/etc/laptop-mode/conf.d/lcd-brightness.conf 文件：
`sudo gedit /etc/laptop-mode/conf.d/lcd-brightness.conf`
修改以下内容：`CONTROL_BRIGHTNESS=1`
`BATT_BRIGHTNESS_COMMAND="echo 3"`
`LM_AC_BRIGHTNESS_COMMAND="echo 3"`
`NOLM_AC_BRIGHTNESS_COMMAND="echo 3"`
`#BRIGHTNESS_OUTPUT="/proc/acpi/video/VID/LCD/brightness"`
 最后一行添加：
 `BRIGHTNESS_OUTPUT="/sys/class/backlight/acpi_video0/brightness"`
（记得要保存文件）
4.最后，执行命令：
`sudo update-grub`

然后，如果上述方法问题无法解决，建议直接下一个ubuntu原生的Brightness
然后色温用gnome的redshift解决

## .crx插件的安装
对于大多数的离线插件，下载完成后打开更多工具>>拓展程序，开启开发者模式，直接拖动即可安装。
少部分是会出现解析错误，把.crx改成.rar或.zip，然后用unzip命令解压后再安装（注意，一定要用终端，否则会有文件缺失）

## 挂载硬盘的暗坑踩坑记录及正确姿势
![一个表情包而以](https://imgconvert.csdnimg.cn/aHR0cHM6Ly93d3cucnVub29iLmNvbS93cC1jb250ZW50L3VwbG9hZHMvMjAxOS8wMS8yMDE5MDExNS0zLmpwZw?x-oss-process=image/format,png)
### 挂载硬盘的正确姿势
查看硬盘分区及大小，确定需要挂的盘：`sudo fdisk -l`

方法1（**mount大法** *适合传文件，用一下就好。或者不限麻烦愿意每次打开文件管理器手动挂载*）：
 1. 暂时挂载可以用mount `sudo mount /dev/sda1 /media`(前一个是要挂的，后一个是挂载位置)
 2. 修改owner `sudo chown -R username:username /media` -R是递归

方法2（**fstab大法** *每次开机自动挂载*）
 1. 获取分区uuid: `sudo blkid`

> 注意：可能会出现
> ```
> /dev/sda1: UUID="DA70A0E270ACFGDR" TYPE="ntfs" PARTUUID="06cdfc10-01"
>/dev/sda5: UUID="C63C5C1B4C543565" TYPE="ntfs" PARTUUID="06cdfc10-05"
> ```
> 你要记住UUID和type**而不仅仅是UUID**！！！！
> 随便在fstab中填type为ext4会导致无法进系统（reboot后会导致ext4 file system崩掉）（别问我怎么知道的）

----

What's the difference between UUID and PARTUUID
A UUID is guaranteed to be unique. As far as I know, collisions will not happen within the lifetime of the universe. However, you'll note that the PARTUUID is much shorter. These are meant to be "locally" unique, and collisions most likely occur between all known PARTUUIDs.

>上述是 https://raspberrypi.stackexchange.com/questions/75027/whats-the-difference-between-uuid-and-partuuid/75030 上一个老哥的回答

----

2. `sudo vim /etc/fstab` 按照这个文件原有的格式，填写UUID, TYPE等保存推出，愉快reboot

----

我是怎么踩坑以及解决的？（按照上述提示的崽崽不会踩这个坑，但如果不幸，你已经像我一样，踩入了这个坑，该怎么做呢？）
**踩坑表现**

 - reboot之后进入不了系统
 - 正常启动ubuntu时持续报错**unsupported event**
 - 正常启动ubuntu时持续报错**can't find ext4 file system**(因为我填错了type)
 - 无法ctrl+D打开shell,  ctrl+alt+2(等等tty终端)打开后依旧**unsupported event** 刷屏
 - recovery mode进入后进入emergency mode,要你键入密码查log，然而，查完了，修复个锤锤哟，还是进不了系统

 如何解决呢？问题很明显是填错了fstab,导致系统出错，所以，**解决方法是把fstab改正确。**
 fstab存在于你的系统盘中，而你自己的系统现在崩了，所以用自己的系统改不太可能。这里如果你有**live usb或者你的ubuntu引导盘**（对，就是你装系统时烧的那个）。
 1. 修改bios，从usb启动。
 2. 不用重装系统，try ubuntu的选项已经提供了供我们使用的OS，点它，进入这个临时的ubuntu系统。
 3. 打开文档管理器，找到你本机的系统盘，记住它的/dev/XXXX位置（用`sudo fdisk -l`命令亦可）(用`ls /dev | grep nvme`亦可)
 4. 如果能用文档管理器打开，就打开吧。打不开的话开sudo，`sudo mount /dev/XXXX /mnt` 暴力挂载（这个姿势的原理：对于你原来的本机系统，这个盘是所需权限高的系统盘，可是对用usb启动的临时系统来说，它只是一个硬盘而已）
 5. `cd /mnt`, `ls`(如果正常，会在/etc下)，`cd /etc`然后`sudo vi fstab`。然后删掉或者修改你写的有问题的部分（UUID没写对的改UUID, TYPE没写对的改TYPE。不知道怎么改的崽，把你添加的删掉或者注释了。`:wq`）
 6. reboot即可（这回就可以进本机系统了QAQ）

----

## 代理姿势
### tty代理(环境变量)

出现了 Failed to connect to 127.0.0.1 port 37389: 拒绝连接的错误？
首先，这个错误是因为走了代理导致的，通过报错可知，是 ：“127.0.0.1 port 37389”。
验证这个想法`env|grep -i proxy`
会出现：
```
HTTPS_PROXY=http://127.0.0.1:37389/
no_proxy=localhost,192.168.20.48
HTTP_PROXY=http://127.0.0.1:37389/
NO_PROXY=localhost,192.168.20.48
```
然后执行
```
unset HTTP_PROXY
unset HTTPS_PROXY
```
即可
在执行完`env|grep -i proxy`后，出现的http_proxy是大小写都有的，在用unset禁止proxy时，大小的也都要有。

`export http_proxy=http://127.0.0.1:8000`
类似这样即可设置环境变量

### apt-get代理

修改apt配置“/etc/apt/apt.conf”

例如
```bash
Acquire::http::proxy "http://127.0.0.1:8000/";
Acquire::ftp::proxy "ftp://127.0.0.1:8000/";
Acquire::https::proxy "https://127.0.0.1:8000/";
```

也可以不使用apt.conf,而指定配置文件
`sudo apt-get -c ~/apt_proxy.conf update`

或者直接设置：
`sudo apt-get -o Acquire::http::proxy="http://127.0.0.1:8000/" update`

### Git代理

```bash
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

只对github
```bash
#只对github.com
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080

#取消代理
git config --global --unset http.https://github.com.proxy
```
### bp代理

首先，把不管是ss,ssr还是v2ray开全局

找到bp的Upstream Proxy Severs(2.0版本：`User options> connections> Upstream Proxt Servers`. 1.6版本：`options> connections> Upstream Proxt Servers`),点击add

然后设置规则

> Destination host: *
> <font color="green">*代表任意个字符或0个字符，?代表除.外的任意一个字符</font>
> Proxy host: 127.0.0.1 <font color="green">代理服务器IP地址，空表示直连</font>
> Proxy port: xxx



## N卡独显大坑

写给对Nvidia又爱又恨的你。

### 显卡驱动自动安装/图形化界面更改显驱
有的朋友更新了内核到18.04，更改了各种conf还无法进入休眠模式可以更新显卡驱动试试
至于16.04，这个内核本身就没有休眠模式，要想避免挂起后无法唤醒的问题，最好的方法就是--禁止挂起！（有个gnome的拓展，叫caffeine，禁止挂起，操作方便又轻量～）
不要用开源的了，N卡非常傲娇，会有各种分辨率问题，搞不好轻则键盘鼠标延时，重则进入不了desktop(~~用tty好像也不错呢~~ )
老老实实用N家的显卡驱动吧。不过网上装显卡驱动文章的很多坑，如果盲目尝试可能又要踩坑了呢~
1. 建议，如果可以，请用**软件与更新**图形界面更改显卡驱动，这个最稳妥。
2. 命令的话，这个比较稳妥: 查看显卡型号和推荐显卡驱动 `ubuntu-drivers devices`；自动安显驱`sudo ubuntu-drivers autoinstall`

### 更新bios后的显示不正常
2019.12.27更新了hp的bios，进入系统后分辨率不正常。查看*软件与更新*，驱动仍然使用nvidia-driver 435, 终端查看nvidia-smi, 显驱联系不上显卡。

这是因为：更新bios后，**secure boot**默认开启，导致第三方源驱动安装被禁止，第三方源驱动使用出现问题。 进入bios, 禁止secure boot(安全启动)，并且清空安全密钥。重启即可。

### 键盘延时？！
有没有这样的体验，显驱很匹配的情况下，偶尔一次两次，你的键盘输入延时了一小会。
这可能是因为nvidia-setting启用了Sync To VBlank（垂直同步）。

>Sync To VBlank 垂直同步：把帧数限制在60帧不超过显示屏刷新频率
>优点：减少无意义浪费。解决屏幕撕裂（如果你有这个问题的话）。
>缺点：可能导致输入延时。（当你着急开发的时候，这个问题尤为要命）

当然你可以自己更改Nvidia setting(谨慎！)，也可以用ccsm来更改
下载`sudo apt-get install compizconfig-settings-manager`
tty键入ccsm打开gui界面，打开General，再打开OpenGL， 取消Sync To VBlank前面的勾勾。

### xrandr报错 和 display resolution
2020.1.23晚上开着win系统就睡觉了，系统自动更新了然后重启，双系统默认启动ubuntu。早上起来发现显示不正常了。

排查问题及修复：
- 首先，看到显示不正常，分辨率有问题，马上看了设置，发现只有默认的一个分辨率的选项无法更改。估计是显卡驱动出了问题。
- 但是查看nvidia-smi一切正常，查看/etc/default/grub文件，`#GRUB_GFXMODE=640x480` 注释很正常，并且查看*软件与更新*，使用的仍然是n家驱动435没有自动更新，没有不匹配。
- 执行`xrandr`, 报错`xrandr: failed to get size of gamma for output default`. 尝试 `killall Xorg`, 发现没有在跑的。
- 并且此时发现系统上没有 */var/log/Xorg.0.log* 和  *.xprofile* 这两个文件，此时推断xorg可能有点问题
重装之 ` sudo apt-get install pkg-config make xutils-dev libtool xserver-xorg-dev libx11-dev libxi-dev libxrandr-dev libxinerama-dev libudev-dev`
- 在askubuntu上，看到一个用*A卡*的人遇到了相似的问题，回答的人说, 是因为他在**messed up专有显卡驱动**的情况下尝试恢复使用该显驱， 所以使用了开源的默认显驱。建议是重装显驱。
我呢，是个之前重装显驱把图形化界面搞崩了的倒霉崽崽，俗话说，一朝被蛇咬，处处闻啼鸟。加之新的440版本是开源的，我用的435是闭源的，干脆一并升级了OS内核和显驱。重启后解决。

反思与总结：

 **xrandr 命令**
xrandr 是一款官方的 RandR (Resize and Rotate)Wikipedia:X Window System 扩展配置工具。它可以设置屏幕显示的大小、方向、镜像、分辨率等。

当没有添加任何选项直接运行时，xrandr 列出该系统可用的显示输出设备 (VGA-1, HDMI-1 等等) 和每一台设备可设置的分辨率，当前分辨率后面带有一个*号和一个+号。

你可以使用 xrandr 设置不同的分辨率（必须是出现在执行 `xrandr` 输出列表中的分辨率）：
xrandr --output HDMI-1 --mode 1920x1080

**xorg 和 x-server**
给个很不错的link自己看吧[这里
](https://blog.csdn.net/seaship/article/details/86233325)

### WekaDeeplearning4j

Env:

weka
Nvidia GPU
CUDA
cuDNN

- Download Weka and install WekaDeeplearning4j

First install java env. I used `openjdk 11.0.18`.

Then install weka, I dowloaded both `3.8.6` and `3.9.6`. 

`java -jar weka.jar` to run weka, and then use Package Manager to install available packages, including `WekaDeeplearning4j`

- Install cuda and cuDNN

Weka needs cuda 10.0 or 10.1 or 10.2

#### NVIDIA official way to install CUDA

ref:

[CUDA installation guide for Linux](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)
[Updating the CUDA Linux GPG Repository Key](https://developer.nvidia.com/blog/updating-the-cuda-linux-gpg-repository-key/)
[cuDNN](https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html)
[WekaDeeplearning4j installation](https://deeplearning.cms.waikato.ac.nz/install/)

**Conclusion: Didn't work for me.**

Check your GPU: `lspci | grep -i nvidia`. Mine is `NVS 310`, it is CUDA capable GPU.

Check your Linux distribution: `uname -m && cat /etc/*release`

Install the kernel headers (and development packages): `sudo apt-get install linux-headers-$(uname -r)`

Download the NVIDIA CUDA Toolkit:

```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda
```
To the new GPG pub key [3bf863cc](https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/3bf863cc.pub) for CUDA repo, install the new cuda-keyring package:

```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
```

Install CUDA SDK and GDS packages

```bash
sudo apt-get update
sudo apt-get install cuda
sudo apt-get install nvidia-gds
sudo reboot now
```

Install CUDA driver

`sudo apt-get install cuda-drivers`

After rebooting, the display is blur.

```bash
lsmod | grep nvidia # only nvidia_fs
nvidia-smi #failed
sudo ubuntu-drivers autoinstall #install nvidia-340
reboot
```

Boot hangs on [ OK ] Started Acounts Service. `Ctrl+Alt+F2` to enter the console.

```bash
sudo apt-get remove --purge '^nvidia-.*'
sudo apt-get install ubuntu-desktop
sudo rm /etc/X11/xorg.conf
reboot
```

Now everything is normal.

#### Install CUDA and cuDNN

[How to install Cuda 10.2, cuDNN 7.6.5 and samples on ubuntu 18.04](https://medium.com/@anarmammadli/how-to-install-cuda-10-2-cudnn-7-6-5-and-samples-on-ubuntu-18-04-2493124478ca)
[Installing CUDA 10.2 or 11.0 on Ubuntu 18.04 or 20.04](https://datacrunch-io.medium.com/installing-cuda-on-your-datacrunch-io-server-8bbc1cf571ee)
[how to install Nvidia driver on ubuntu 20.04](https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-ubuntu-20-04-focal-fossa-linux)

Download Nvidia driver from [here](http://www.nvidia.com/Download/index.aspx)

For me, it is `NVIDIA-Linux-X86_64-390.157.run`.

`sudo apt install build-essential libglvnd-dev pkg-config`

Disable Nouveau Nvidia driver.

```bash
$ sudo bash -c "echo blacklist nouveau > /etc/modprobe.d/blacklist-nvidia-nouveau.conf"
$ sudo bash -c "echo options nouveau modeset=0 >> /etc/modprobe.d/blacklist-nvidia-nouveau.conf"
$ cat /etc/modprobe.d/blacklist-nvidia-nouveau.conf
blacklist nouveau
options nouveau modeset=0
$ sudo update-initramfs -u
$ sudo reboot
```

Stop Desktop Manager `sudo telinit 3`

`CTRL+ALT+F1` and then login.

```bash
sudo bash NVIDIA-Linux-x86_64-440.44.run
reboot
```

Install CUDA

```bash
nvidia-smi
git clone https://github.com/DataCrunch-Scripts/Install-CUDA.git
cd ./Install-CUDA
chmod +x installer.sh
sudo bash installer.sh
sudo apt install nvidia-cuda-toolkit
```

Check CUDA

```bash
nvcc --version
systemctl status nvidia-persistenced
# enable the daemon
sudo systemctl enable nvidia-persistenced
cat /proc/driver/nvidia/version
nvidia-smi
```

Because `apt` doesn't install packages under prefix `/usr/local`, but for cuDNN, we need it under this path. So we need to create a symlink.

Find the path where CUDA is installed: `locate nvcc`. For me, it is `/usr/lib/nvidia-cuda-toolkit`. Thus, create the symlink `sudo ln -s /usr/lib/nvidia-cuda-toolkit/ /usr/local/cuda`

And there is another conflict, the most suitable Nvidia driver for this env is 390, but for 390, it needs CUDA version lower than 9.1. But here, I used CUDA 10.1.

I checked on Nvidia's website, for CUDA 10.1, Linux x64, the driver need to be >= 418.39, so I installed `418.56`. And Nvidia didn't support NVS 310 since the release if driver 390. But also, `NVS 310` supports CUDA. Seems a paradox.

`nvidia-settings` to conf Nvidia driver

Download and install cuDNN [here](https://developer.nvidia.com/cudnn)

I actually used cuDNN for 18.04 version, because weka only support cuda 10.1, 10.2 etc

```
cuDNN Runtime Library for Ubuntu20.04 x86_64 (Deb)
cuDNN Developer Library for Ubuntu20.04 x86_64 (Deb)
cuDNN Code Samples and User Guide for Ubuntu20.04 x86_64 (Deb)
```

Add GPU support for Weka as mentioned in [WekaDeeplearning4j installation](https://deeplearning.cms.waikato.ac.nz/install/).


## v2ray配置

网上有很多一键配置的jio本，如果想一键配置在此就不多赘述了，自己搜吧。这里记录下手动安装的过程及遇见的问题

1. 下载`wget https://github.com/v2ray/v2ray-core/releases/download/v3.24/v2ray-linux-64.zip`
2. 下一步是解压缩后进入目录，移动文件位置
创建目录`mkdir /usr/bin/v2ray  /etc/v2ray/`
移动文件位置
```bash
cp v2ray /usr/bin/v2ray/v2ray
cp v2ctl /usr/bin/v2ray/v2ctl
cp geoip.dat /usr/bin/v2ray/geoip.dat
cp geosite.dat /usr/bin/v2ray/geosite.dat
cp vpoint_vmess_freedom.json /etc/v2ray/config.json
```
3.生成service
这一步是生成systemctl service的关键
找到v2ray下`systemd/v2ray.service`，cp到`/lib/systemd/system` 或者 `/etc/systemd/system`下。这一步和你自己之前的配置有关,看看你自己的.service文件都放在哪个路径下了。

4.手动添加log
```bash
mkdir /var/log/v2ray/
touch /var/log/v2ray/access.log
touch /var/log/v2ray/error.log
touch /var/run/v2ray.pid
```
至此，v2ray安装完毕
检验：
```bash
systemctl start v2ray
systemctl status v2ray
```

将其设置为系统自动启动` systemctl enable v2ray`

## Appimage

### Cannot run due to existing symlinks in /tmp (FIXME)

用QQ的appimage时多次打开关闭出现该报错

Needs to be fixed in the AppImage AppRun script.
Need to `rm /tmp/ld-linux.so.2`

### 删除menu entries

appimage无需安装，也就无需卸载，当不用的时候，把这个file删掉就行。
有时删除后，menu entry仍然存在。
debian系中，可以在`/home/$USER/.local/share/applications`找到menu entries, 删除对应的即可。

## Lua包管理，luarocks

在使用Lua的过程中遇到了少module的报错，本着以后方便的想法打算直接装包管理luarocks

```bash
wget https://luarocks.org/releases/luarocks-3.3.0.tar.gz
tar zxpf luarocks-3.3.0.tar.gz
cd luarocks-3.3.0
./configure && make && sudo make install
sudo luarocks install luasocket
lua
Lua 5.3.5 Copyright (C) 1994-2018 Lua.org, PUC-Rio
> require "socket"
```

安装的时候有一个小坑，报错缺少`lua.h`
由于我之前使用`z.lua`,安装了lua5.2,这里还要安装一下`lua5.3`（直接`apt install`即可）
然后`sudo apt install liblua5.3-dev`,这个包里面有`lua.h`

## burpsuite抓https包

其实是个很简单的事情，bp下载CA证书(无论是在`http://burp`还是在` Proxy > Options > Proxy Listeners > Import / export CA certificate`都可)， 然后导入浏览器即可。
但是偏偏我遇到了一个问题，就是无论怎样，下载的CA 证书都是0 byte, 这解析个锤锤哟。
[这里](https://forum.portswigger.net/thread/ssl-certificate-2d285027ba60d5457e3e)是在官网上看到的和我遇到的一模一样的问题。

> Okey i discovered the problem.
Im was using a beta version pro 1.6, i installed the 1.7 free version and now i can download my cert.

好巧不巧，我用的也是bp pro 1.6,所以这是个版本问题么...总之有点意思，下了新的版本就解决了。

## ubuntu播放mp4

The reason you get the error is because your Ubuntu desktop is missing the required codecs or decoders. The video you’re trying to watch is using a copy-right protected technology and Ubuntu is not designed to play them.

You must install these packages below in order to play those videos. Run the commands below to install the missing codecs and decoders from Ubuntu Desktops.

```bash
sudo apt install libdvdnav4 libdvdread4 gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly libdvd-pkg
sudo apt install ubuntu-restricted-extras
```

## vbox中虚拟机使用宿主机代理

参考：
https://www.cnblogs.com/sakam0to/p/10627524.html
https://blog.csdn.net/bytxl/article/details/35569217

VB默认使用NAT(Network Address Translation),它允许一个整体机构以一个公用IP地址出现在Internet上。
这时，VB为电脑安装虚拟网卡，虚拟机的网络请求发到这个网卡上，再通过宿主机的真是网卡连上网络。不经过宿主机的代理。

所以要将虚拟机设置为使用桥接模式，使宿主机作为网桥。

vbox>>要改的虚拟机>>设置>>网络>>连接方式>>桥接网卡

可能需要手动分配IPV4地址给虚拟机。

然后设置虚拟机代理即可。(同时我在想，如果宿主机是使用mellow这样的透明代理，是不是直接选桥接模式就可以了呢？没有验证过，如果以后用mellow的话可以试一试)

## Ubuntu安装jdk1.8及多jdk管理

JDK在linux有两个版本，一个开源版本Openjdk(比如ubuntu默认的java11就是openjdk)，还有一个oracle官方版本jdk。

oracle JDK既可以通过添加ppa源命令行安装，也可以去官网下载jdk压缩包安装。

----

### ppa安装

`sudo apt-get install python-software-properties`安装依赖
`sudo add-apt-repository ppa:webupd8team/java`添加ppa
`sudo apt-get update`
`sudo apt-get install oracle-java8-installer`
接受协议即可

----

----

### oracle官网安装

用[官网](https://www.oracle.com/java/technologies/javase-downloads.html)下载也可。
过程可以参考[这篇博客](https://blog.csdn.net/m0_37921080/article/details/79903448)。
唯一的问题是要注册oracle的账号，好麻烦。

----

### 安装openjdk-8-jdk


`sudo apt-get install openjdk-8-jdk`
查看安装路径`dpkg -L openjdk-8-jdk`
对于我来说，我可以看到`/usr/lib/jvm/java-8-openjdk-amd64`等

接下来配置环境变量`sudo vim .bashrc`

```bash
#配置openjdk8环境变量
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64  
export JRE_HOME=${JAVA_HOME}/jre  
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  
export PATH=${JAVA_HOME}/bin:$PATH
```

重新打开tty，`java -version`就可以愉快看见配置成功了。

### 配置多版本

然后就可以愉快配置多版本了。

查看所有jdk安装版本`sudo update-java-alternatives -l`

`sudo update-java-alternatives -s [java版本]`即可切换。

## Java bug

系统: ubuntu 18.04和20.04
内核版本：4.15-rc1、5.7-rc7

Java环境：8，11，17， openJDK和Oracle。

从16.04升级到18.04时出现了这个问题，然后在升级到了20.04仍然有这个问题。

launchpad 上的 bug discription: *Java desktop application freezes with openjdk 8u252*

https://bugs.launchpad.net/ubuntu/+source/openjdk-8/+bug/1880246

> **JDK** (Java Development Ki) is a software development environment used for developing Java applications and applets.It includes the Java Runtime Environment (JRE), an interpreter/loader (Java), a compiler (javac), an archiver (jar), a documentation generator (Javadoc), and other tools needed in Java development.
> JRE: Java Runtime Environment
> JVM: java virtual machine is responsible for executing the java program line by line, hence it is also known as an interpreter.

Arduino IDE uses Java as well, so it freezed from time to time. When looking through Intellij's forum, I saw this post:
https://intellij-support.jetbrains.com/hc/en-us/community/posts/360008276240-Frequent-freezes-and-crashes-in-Ubuntu-20-04

> This has been fixed for me since update to this version (using built-in JRE):

So I searched on Arduino's website and found THIS
https://support.arduino.cc/hc/en-us/articles/4410177782418-If-the-Arduino-IDE-freezes-or-is-unresponsive
I uninstalled the IDE and deleted the folders and reinstalled it, and the it never freezes again.

Thus, I discovered more about this problem. After uninstalling, I still found `Arduino/` and `.arduino15/` in `~`. Since I tried reinstalling withou deleting these folders, the bug still appeared. So those are the keys to fix the bug.

In both paths, there are libs inside. In `Arduino/`, only a `readme.txt` in `libraries/`. In `.arduino15/`, however, I can see THIS

```bash
$ cat preferences.txt | grep java
preproc.imports.list=java.applet.*,java.awt.Dimension,java.awt.Frame,java.awt.event.MouseEvent,java.awt.event.KeyEvent,java.awt.event.FocusEvent,java.awt.Image,java.io.*,java.net.*,java.text.*,java.util.*,java.util.zip.*,java.util.regex.*
```

I think that's the point.

## vmware

### 无法reinstall vmware tools

三种方法。

1. CD/DVD设置成自动检测，如果没有，就创建。重启后CD/DVD connect,就可以看到vmware tools的相关工具

2. `whereis vmware`找路径， `/usr/lib/vmware/isoimages`路径下有linux.iso, windows.iso(建议把这两个cp到其他dir)
根据虚拟机操作系统，`setting>hardware>CD/DVD`使用对应的iso,重启。

3. 如果第二个无效,binwalk解包对应的iso,解出来的vmware-install.pl放进虚拟机里面运行。(可以加上选项`--default`)

## Virtual Box

### 多个vmdk合成一个

用vmware的人导出的vmdk很多情况下是`s001.vmdk`这种情况，对于linux下的vbox users, 这样当然是导入不成的，要合并成一个才行。（用`cat`当然是不行的。）

对于vmware users 只要执行`"C:\Program Files (x86)\VMware\VMware Player\vmware-vdiskmanager.exe" -r "d:\VMLinux\vmdkname.vmdk" -t 0 MyNewImage.vmdk`即可。

对于linux user, 如果需要使用qemu的镜像格式，把多个vmdk转成qcow2，可以参考[这里](https://askubuntu.com/questions/4398/how-do-i-convert-a-multiple-part-vmdk-disk-image-to-qcow2)

linux下不用vmware直接合成一个的方法我目前还没有找到。

### vbox failed to import appliance

----

equipment, device, appliance区分

- **equipment**: 特定活动所需的设备、器械，*un*.
一件设备:<font color="blue"> a piece of equipment</font>
Equipment通常指成套的，不只一件的设备。与device和appliance不同，equipment 不光包括电子设备，还包含相关的工具。
医疗设备: <font color="blue">medical equipment</font>
听诊器stethoscope是一种medical equipment, 但它并不是一个medical device，因为听诊器不是电子的。
*e.g.The hospital has been donated medical equipment that’s worth a million pounds.*

- **device**通常指小巧的电子装置或设备, *cn*.
移动设备: <font color="blue">mobile device</font>
听力装置: <font color="blue">listening device</font>
*e.g.All mobile devices should be switched off during this flight.*

- **Appliance**由指家用电器home appliances, *cn*，比如冰箱、烤箱、洗衣机等等。
通常，冰箱本身并不是device，但可以把控制家电的智能家居设备叫做<font color="blue">home device。</font>
*e.g.The shopping channel is known for selling home appliances.*
----

#### Image file corrupt

This happens because of network issues during the download or the file is not downloaded completely.

To resolve the error we re-download the file and try to import the file.

#### Attach as a virtual hard disk

In this case, the file downloaded properly, but still facing the same error.
Here, we create a new VM and attach the file as a virtual disk.
We open Virtualbox Manager and click on New.
Now we enter the Name, Type, and version of the operating system and click next.
Then we select the Allocated memory size and click next.
Select the option Use an existing virtual hard disk file. Now we browse and locate the file. Click on Create.
Thus it creates a new virtual machine with the attached file.

#### Administrative privileges for vboxmanage.exe

Another common reason for import appliance failure in **Windows** happens when the vboxmanage.exe file does not have the administrative privileges.
This occurs when trying to *attach the disk from the USB drive*. This is because the USB drive requires admin rights. So our Support Engineers run the application as an administrator and import Appliance in VirtualBox.

#### Corrupted VirtualBox installation

The corrupted VirtualBox installation will also fail to import appliance. During corrupted VirtualBox, the only option is to re-install the whole VirtualBox. So our Support Engineers re-install the VirtualBox once again and import the appliance.

## vim

### Ubuntu下的Markdown编辑器和markdown-toc

之前，在我还用atom的时候，安了markdown的插件就没再管过，但是atom太慢了。后来我写代码主要是用vim了,就想着再装一个markdown editor.

首先我用了韩国的haroopad,支持中文版和`[TOC]`,可以export到html和pdf,但是对中文字体的支持不好，那个字体看得难受。并且有只能显示一个mermaid Graph的bug。

后来用了remarkable, 真是清爽。又轻量,界面又舒服，添加[markdown-toc](https://github.com/jonschlinkert/markdown-toc) 即可使用`[TOC]`，唯一美中不足的是，每次更新目录都要re-run markdown-toc
在项目内安装markdown-toc ` npm install --save markdown-toc`
每次运行 `npx markdown-toc README.md`
但是问题是，没办法直接像haroopad那样直接复制有style的html(虽然写了这个功能，但复制的结果就是markdown格式的QAQ)

所以最后还是vim吧，vim插件们不香么。

1. 首先，添加实时预览 在`.vimrc`中添加plugin.(我用的包管理是vundle)

```
Plugin 'iamcco/mathjax-support-for-mkdp'
Plugin 'iamcco/markdown-preview.vim'
```

然后在`.vimrc`的末尾添加预览的快捷键映射

```
nmap <silent> <F8> <Plug>MarkdownPreview        " for normal mode
imap <silent> <F8> <Plug>MarkdownPreview        " for insert mode
nmap <silent> <F9> <Plug>StopMarkdownPreview    " for normal mode
imap <silent> <F9> <Plug>StopMarkdownPreview    " for insert mode
```

然后安装plugin们。

意思是说，在普通模式下（n）和插入模式下（i），按下F8键就可以实时预览，按下F9键就可以停止预览。(用浏览器预览，很Nice)
还挺好看的，不过也不支持[TOC]

2. 接下来就添加生成TOC的plugin
[vim-markdown-toc](https://github.com/mzlogin/vim-markdown-toc)的详细说明

在`.vimrc`中添加`Plugin 'mzlogin/vim-markdown-toc'`,然后install

用法：把光标移动到想放的位置，然后键入

```
:GenTocGFM
:GenTocRedcarpet
:GenTocMarked
:GenTocGitLab
```

### Spacevim大坑

搞java开发看人安利了spacevim，就以为那是个plugin,安了。哪想到 `.vim->.Spacevim` orz
好吧，幸好安装时有backup, `curl -sLf https://spacevim.org/install.sh | bash -s -- --uninstall`之后就开始恢复vim
首先根据备份把.vim/和.vimrc恢复到~/

----

我遇到一个小问题，之前我把这些`*_back`都mv到了我自己作备份用的文件夹，在未卸载spacevim时执行`cp .vimrc_back ~/.vimrc`之后，在~/还是找不到.vimrc
然后我在他们官网找到了答案

> Can I try SpaceVim without overwriting my vimrc?
The SpaceVim install script will move your ~/.vimrc to ~/.vimrc_back. If you want to have a try SpaceVim without overwriting your own Vim configuration you can:
>
> Clone SpaceVim manually.
>
> git clone https://github.com/SpaceVim/SpaceVim.git ~/.SpaceVim
> Then, start Vim via vim -u ~/.SpaceVim/vimrc. You can also put this alias into your bashrc.
>
> alias svim='vim -u ~/.SpaceVim/vimrc'

啊我的心好痛
这件事告诉我一个道理：用专门的dir作备份，恢复时用cp不用mv

----

恢复完了就是无尽的报错

```
处理 function down_quote_syntax#enable_quote_syntax[7]..markdown_quote_synta
x#include_other_syntax 时发生错误:
第    9 行:
E484: 无法打开文件 syntax/coffee.vim
E484: 无法打开文件 syntax/mustache.vim
```

你品，你细品，这些个东西还损坏了，重新install吧。

总结一句，spacevim比较适合vim小白，它更像是个配置好的ide而不是你独一无二的vim.对于一个vimer来说，所有的.vimrc都是经过了时间和不断的使用找出来的最适合自己的配置。与其你去熟悉去适应某个ide的用法，不如使editor去适应你。这大概也是大家喜欢vim的原因吧。

## mega下载占盘太多

2020/09/27

今天下一个2G的大文件，突然发现/只剩200M了。我立刻意识到这是因为下载的缘故，此时去下载历史里看，没有出现这个文件。find去`/`找`.mega`也没有找到。
所以这个下了一半的file哪儿去了？

要回答这个问题，要先知道mega是怎么下载的。https://webapps.stackexchange.com/questions/41068/how-exactly-does-megas-download-work#:~:text=When%20you%20download%20a%20file,normal%20download%20process%20is%20started.

> When you download a file from the MEGA service, you are shown a pretty download progress bar within the browser. Once this progress bar reaches 100%, your browser then begins to download the file. That is, only once the graphical download is complete, your browser's normal download process is started.> It uses the fileSystem API, which basically writes the file to a sandboxed section of your local file system:
> AppData\Local\Google\Chrome\User Data\Default\File System\ (显然，这是win)
> It is "Resumable" downloads, but not being able to choose your download folder isn't ideal.

我然后去查了`~/.cache/google-chrome`,也看到什么，索性`rm -R Default/`。

在`/`下`find . -type f -size +800M`找到了
`~/.config/google-chrome/Default/File System/320/p/00/00000000`，终于我看到了那个1013M的file。
以及很罪恶的是，除了320还有别的,怪不得mega可以一直知道我下了多少，然后接着下，不像其他的要从头下。
`rm -R 3*`
舒服了～

9-29上午，收到了mega support的邮件
> It's stored in your browser's temporary storage.
> You can simply clear your browser cache for https://mega.nz by navigating to chrome://settings/content/siteDetails?site=https%3A%2F%2Fmega.nz%2F and clicking "Clear data"

## gnome

### Ubuntu gnome 美化

`sudo apt-get install gnome-tweak-tool`

### chrome安装gnome extension

Add chrome extension.
https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep

`sudo apt install chrome-gnome-shell`

### gnome录屏

gnome自带录屏功能，`Ctrl+Alt+Shift+R`开始/结束录屏，默认时间30s就会结束。
`gsettings set org.gnome.settings-daemon.plugins.media-keys max-screencast-length 0`修改录屏时间为不限制时间。这里，最后的数字表示允许录屏的时间，单位为s,如果是0就表示不限制。

## wine qq

### 安装

安装 wine

```
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install wine-stable
```

安装wine应用
`sudo dpkg -i xxx.deb`

wine-qq下载地址
https://www.ubuntukylin.com/applications/23-cn.html

deepin的qq（最新版本和老一个版本）我用不了，能出来扫码登录的页面但是不能登录成功，可以使用安装的文件夹中的uninstall.sh卸载，然后`dpkg -l | grep deepin`卸载其它的。

原生的linux qq总是登录后就闪退，2020年12月以来，按照官方的闪退解决方法也无法解决闪退问题了。

优麒麟wine-qq也挺慢的，而且很卡，经常操作两下就无响应了。

总之，都不好用。

### wine-qq文件下载路径

~/.wineqq/drive_c/users/你的用户/My Documents/Tencent Files/对应QQ号/FileRecv

## 娱乐

### cmus
|操作|命令|
|---|---|
|导入音乐|:a /music/pach/
|播放或重播音乐|x
|暂停|c
|播放下一首音乐|b
|播放上一首音乐|z
|激活随机播放|s
|清空当前文件列表|:clear
|保存播放列表|:save /path/to/playlist
|加载播放列表|:load /path/to/playlist
|在7个不同的功能界面之间切换|数字键1-7
|退出播放器|q

## xampp

```
chmod 755 xampp-linux-*-installer.run
sudo ./xampp-linux-*-installer.run
```

lampp start
```
sudo /opt/lampp/lampp start
```

## Install ROS on Ubuntu 20.04

> ROS (Robot Operating System) provides libraries and tools to help software developers create robot applications. It provides hardware abstraction, device drivers, libraries, visualizers, message-passing, package management, and more. ROS is licensed under an open source, BSD license.

> ROS Noetic Ninjemys is primarily targeted at the Ubuntu 20.04 (Focal) release

[Ubuntu install of ROS Noetic](https://wiki.ros.org/noetic/Installation/Ubuntu)

Installation:

```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -

sudo apt update

# Desktop-Full Install
sudo apt install ros-noetic-desktop-full
```

Source sh (bash here) before using ROS

```bash
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

Install dependencies.

```bash
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```

### Use ROS's dependency management tool rosdep 

> rosdep is a command-line tool for installing system dependencies. It is ROS’s dependency management utility that can work with ROS packages and external libraries.

[Managing Dependencies with rosdep](https://docs.ros.org/en/humble/Tutorials/Intermediate/Rosdep.html)

Initialize rosdep when using for the first time.

```bash
sudo rosdep init
rosdep update
```

Install dependencies with rosdep

```bash
rosdep install --from-paths src -y --ignore-src
```

### Build catkin workspace

[Creating a workspace for catkin](https://wiki.ros.org/catkin/Tutorials/create_a_workspace)

```bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
source devel/setup.bash #source the new setup.sh
echo $ROS_PACKAGE_PATH #make sure ROS_PACKAGE_PATH environment variable includes the directory you're in
```


### Install ROS driver to communicate with parrot drones


To use HKSSY's Drone-Hacking-Tool

[bebop_autonomy - ROS Driver for Parrot Bebop Drone (quadrocopter) 1.0 & 2.0](https://bebop-autonomy.readthedocs.io/en/latest/)

> bebop_autonomy is a ROS driver for Parrot Bebop 1.0 and 2.0 drones (quadrocopters)

[Installation of bebop_autonomy](https://bebop-autonomy.readthedocs.io/en/latest/installation.html)

Pre-requirements.

```bash
sudo apt-get install build-essential python3-rosdep python3-catkin-tools
```

Check ROS distro `echo $ROS_DISTRO`

Install [parrot_arsdk wrapper](https://github.com/antonellabarisic/parrot_arsdk/tree/noetic_dev)(for Ubuntu 20.04 and ROS noetic)
