---
title: NAS系统选择与重复文件删除体验
date: 2020-02-27 14:46:34
category: 瞎折腾
tags: NAS
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/02/27/deduplication.png
---

## 需求分析

前段时间，网上瞎买了些电子垃圾，动手组装了台 NAS , 开始打算用 FreeNas 系统组 ZFS 阵列。但是在看了 ZFS 的各种文档后发现 ZFS 虽然有着诱人的容量和性能的体验，但是却非常的消耗系统资源。此外 ZFS 的扩容方式和常见的 Raid 阵列都不一样，并不方便直接向存储池中添加磁盘。由于穷，没钱一次性买那么多硬盘，加之组装的 NAS 走的低功耗路线，性能相当菜（双核奔腾5400的CPU，加上8G内存），因此果断放弃。

- 现在手里的硬件平台：
    - G5400双核的CPU +8G内存
    - 两块 4T 日立机械硬盘
    - 8 盘位的机箱

- 罗列了下自己的需求
    - 一个安全为主的存储池和一个性能较好的存储池
    - 方便扩容的磁盘阵列
    - 重复文件删除和 SSD 缓存加速
    - SMBA3 和 NFS 的文件共享需要

根据自己的计划，先利用两个盘位搭建一个安全为主的存储池用于存放相片等资料，剩余6个盘位等以后有钱了慢慢组 Raid5。

<br>

## 系统选择

在网上逛了一圈，花了几天体验了包括黑群在内的诸多NAS系统，发现 Linux 平台除了 ZFS 均无法实现文件系统级别的重复文件删除。而 SSD 缓存加速也需要复杂的软件配置。FreeNas打头的 ZFS 以及其底层的 FreeBSD 系统较为难用，不适合家庭使用。唯一比较接近目标的黑群，又因为对万兆网卡（以后打算上）的兼容问题以及盗版系统的种种强迫症问题让我放弃选择。

回头看 Windows 平台，Server 版本的系统虽然具有重复文件删除的功能，但 Windows 对 raid 的支持明显没有 Linux 下那么完整，（例如无法支持 Raid6，可靠性不如 mdadm 等）

具体不同平台阵列的情况可以看下图（来自知乎@awpak78）

[![datapool.jpg](https://media.everdo.cn/tank/pic-bed/2020/02/27/datapool.jpg)](https://up.media.everdo.cn/image/99B)

至于 Winserver 分层缓存的奇偶校验存储池也因为上手门槛过高让小白的我难以下手。【DOG/哪个dalao会可以教教我】

在看了不少 Dalao 使用 Vmware 虚拟机操作系统 esxi 装 NASos 的文章后，我突然想到，或许可以使用免费开源的虚拟机系统 PVE（ProxmoxVE）来替代 esxi ，使用 linux 的 mdadm 来创建管理 raid 磁盘阵列。因为 PVE 系统基于 Debian ，虽然我之前习惯了 Centos ，但上手起来也没有太大的难度。

在 PVE 系统使用 mdadm 创建 RAID,然后使用 VT 硬件虚拟化，将 /dev/md0 磁盘阵列硬件直通到虚拟机的 WinServer 中，然后在 Windows 中创建 NTFS 或者 REFS 文件系统，并对之开启重复文件删除功能。至于 SSD 缓存加速则可以使用 Primocache 来实现。

这波方案虽然绕了点，却完美满足需求诶！！！

<br>

## 配置完成

在装好系统后，我先用手里的两个盘创建了 RAID1 阵列。

[![mdadm.jpg](https://media.everdo.cn/tank/pic-bed/2020/02/27/mdadm.jpg)](https://up.media.everdo.cn/image/EOt)

qm 命令配置直通给 Windows 后一切正常

![fde3b5ec6d6be8546f04d5d40db8c536.jpg](https://media.everdo.cn/tank/pic-bed/2020/02/27/fde3b5ec6d6be8546f04d5d40db8c536.jpg)

成功创建文件系统，并拷入自己的数据

[![vdisk.jpg](https://media.everdo.cn/tank/pic-bed/2020/02/27/vdisk.jpg)](https://up.media.everdo.cn/image/sxI)

需要注意的是，在 PVE 下运行的虚拟机是采用 KVM 虚拟化的，搭配 VirtIO 半虚拟化技术才能发挥最佳性能。因此这里也费力些功夫将硬件配置为 QEMU HARDDISK。

<br>

## 重复文件删除体验

终于到了核心功能重复文件删除了。为什么采用重复文件删除？还得从我的懒习惯说起，我备份数据向来是想到的时候随手一复制，往往出现一份数据备份好几遍的情况【尴尬】。

有了重复文件删除功能，可以说解决了我老大难的问题了！

在 WinServer 系统中启用这项功能很简单，只要先为服务器添加这项功能，然后对卷启用就可以了。

![jiaosegn.jpg](https://media.everdo.cn/tank/pic-bed/2020/02/27/jiaosegn.jpg)

安装完功能进行一次重启，然后配置开启重复文件删除

[![cfwjsc1.jpg](https://media.everdo.cn/tank/pic-bed/2020/02/27/cfwjsc1.jpg)](https://up.media.everdo.cn/image/Md4)

可以看到刚开启的时候，重复文件删除率是0

因为系统是通过计划任务定时执行重复文件删除操作的，未来更快体验到效果，我使用下面的 Powershell 命令来手动运行一次优化任务。

以下的 Powershell 命令可以从微软官方文档中寻找到

>链接地址：[官方文档](https://docs.microsoft.com/zh-cn/powershell/module/deduplication/start-dedupjob?view=win10-ps)

[![cfwjsc2.jpg](https://media.everdo.cn/tank/pic-bed/2020/02/27/cfwjsc2.jpg)](https://up.media.everdo.cn/image/v0M)

以下是我的操作，先导入 Powershell 命令模块

```powershell
PS C:\> Import-Module ServerManager
PS C:\> Import-Module Deduplication
```

然后运行 Start-DedupJob 命令开始优化（Volume后面的值改成自己需要优化的卷）

```powershell
PS C:\> Start-DedupJob –Volume D: –Type Optimization
```
根据官方文档，还可以使用 **Get-DedupJob** 命令查询进度

[![cfwjsc3.jpg](https://media.everdo.cn/tank/pic-bed/2020/02/27/cfwjsc3.jpg)](https://up.media.everdo.cn/image/y8Y)

输完命令，静静等待奇迹发生吧！

[![cfwjsc4.jpg](https://media.everdo.cn/tank/pic-bed/2020/02/27/cfwjsc4.jpg)](https://up.media.everdo.cn/image/XFa)

可以看到任务由 Queued 转为 Running ，然后我听到了震耳欲聋的炒黄豆的声音（机械硬盘声音贼大！！！）

一个小时后……

[![cfwjsc5.jpg](https://media.everdo.cn/tank/pic-bed/2020/02/27/cfwjsc5.jpg)](https://up.media.everdo.cn/image/C9s)

已经可以通过GUI看到优化完成后的文件系统，居然已经删除了 103GB 的重复文件！！节省了大量的磁盘空间。可以说是穷买不起硬盘党的福音哇！

另外这种文件系统级别的重复文件删除不是真的把重复的两份文件直接删除，而是利用了像C语言里的指针类似的技术（emm，不知道理解的对不对），将重复的数据块指向相同的磁盘空间，从而节省磁盘空间。所以原先的文件目录结构等都不会发生变化。

NICE!! 巨硬打法好！

[![Windows-server-2019.jpg](https://media.everdo.cn/tank/pic-bed/2020/02/27/Windows-server-2019.jpg)](https://up.media.everdo.cn/image/SU3)