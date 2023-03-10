---
title: Docker 基础知识
author: yinuuu
date: 2023-2-19
categories:
  - Tools
tags:
  - Docker
sticky: 2
---


# 1 什么是Docker

**Docker**是一个[开放源代码](https://zh.wikipedia.org/wiki/%E9%96%8B%E6%94%BE%E5%8E%9F%E5%A7%8B%E7%A2%BC)软件项目，让应用程序部署在[软件货柜](https://zh.wikipedia.org/wiki/%E4%BD%9C%E6%A5%AD%E7%B3%BB%E7%B5%B1%E5%B1%A4%E8%99%9B%E6%93%AC%E5%8C%96)下的工作可以自动化进行，借此在[Linux](https://zh.wikipedia.org/wiki/Linux)操作系统上，提供一个额外的软件[抽象层](https://zh.wikipedia.org/wiki/%E6%8A%BD%E8%B1%A1%E5%B1%A4)，以及[操作系统层虚拟化](https://zh.wikipedia.org/wiki/%E4%BD%9C%E6%A5%AD%E7%B3%BB%E7%B5%B1%E5%B1%A4%E8%99%9B%E6%93%AC%E5%8C%96)的自动管理机制

依据行业分析公司“451研究”：“Dockers是有能力打包应用程序及其虚拟容器，可以在任何Linux服务器上运行的依赖性工具，这有助于实现灵活性和便携性，应用程序在任何地方都可以运行，无论是公有云、私有云、单机等。”

**简单来说,Docker 通过对应用组件的封装、分发、部署、运行等生命周期的管理，使用户的APP（可以是一个WEB应用或数据库应用等等）及其运行环境能够做到“一次封装，到处运行”。**

# 2 为什么 Docker 如此流行?

一款产品从开发到上线，从操作系统，到运行环境，再到应用配置。作为开发+运维之间的协作我们需要关心很多东西，这也是很多互联网公司都不得不面对的问题，特别是各种版本的迭代之后，不同版本环境的兼容，对运维人员都是考验。Docker之所以发展如此迅速，也是因为它对此给出了一个标准化的解决方案。

环境配置如此麻烦，换一台机器，就要重来一次，费力费时。很多人想到，能不能从根本上解决问题，软件可以带环境安装？也就是说，安装的时候，把原始环境一模一样地复制过来。开发人员利用 Docker 可以消除协作编码时“在我的机器上可正常工作”的问题。

![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525135454.png#crop=0&crop=0&crop=1&crop=1&id=WNk84&originHeight=350&originWidth=707&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

之前在服务器配置一个应用的运行环境，要安装各种软件，随便拿一个 Java 项目来说，Java/Tomcat/MySQL/JDBC驱动包基本是必不可少的。安装和配置这些东西有多麻烦就不说了，它还不能跨平台。假如我们是在 Windows 上安装的这些环境，到了 Linux 又得重新装。况且就算不跨操作系统，换另一台同样操作系统的服务器，要移植应用也是非常麻烦的。

传统上认为，软件编码开发/测试结束后，所产出的成果即是程序或是能够编译执行的二进制字节码等(java为例)。而为了让这些程序可以顺利执行，开发团队也得准备完整的部署文件，让维运团队得以部署应用程式，开发需要清楚的告诉运维部署团队，用的全部配置文件+所有软件环境。不过，即便如此，仍然常常发生部署失败的状况。

**Docker镜像的设计，使得Docker得以打破过去「程序即应用」的观念。透过镜像(images)将作业系统核心除外，运作应用程式所需要的系统环境，由下而上打包，达到应用程式跨平台间的无缝接轨运作。**

# 3 Docker 的理念

Docker是基于Go语言实现的云开源项目。

Docker的主要目标是“Build，Ship and Run Any App,Anywhere”，也就是通过对应用组件的封装、分发、部署、运行等生命周期的管理，使用户的APP（可以是一个WEB应用或数据库应用等等）及其运行环境能够做到“一次封装，到处运行”。

![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525135659.png#crop=0&crop=0&crop=1&crop=1&id=iKHLj&originHeight=293&originWidth=645&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

Linux 容器技术的出现就解决了这样一个问题，而 Docker 就是在它的基础上发展过来的。将应用运行在 Docker 容器上面，而 Docker 容器在任何操作系统上都是一致的，这就实现了`跨平台、跨服务器`。只需要一次配置好环境，换到别的机子上就可以一键部署好，大大简化了操作(可以参考一下 Java 的一次编译,处处运行特性)

> 简单来说,Docker 的出现解决了运行环境和配置问题软件容器，方便做持续集成并有助于整体发布的容器虚拟化技术


# 4 Docker 虚拟化

-  虚拟机技术
虚拟机（virtual machine）就是带环境安装的一种解决方案。 它可以在一种操作系统里面运行另一种操作系统，比如在Windows 系统里面运行Linux 系统。应用程序对此毫无感知，因为虚拟机看上去跟真实系统一模一样，而对于底层系统来说，虚拟机就是一个普通文件，不需要了就删掉，对其他部分毫无影响。这类虚拟机完美的运行了另一套系统，能够使应用程序，操作系统和硬件三者之间的逻辑不变。
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525140019.png#crop=0&crop=0&crop=1&crop=1&id=iSYFB&originHeight=473&originWidth=342&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
虚拟机的缺点： 
   1. 资源占用多
   2. 冗余步骤多
   3. 启动慢
-  容器虚拟化技术
由于前面虚拟机存在这些缺点，Linux 发展出了另一种虚拟化技术：Linux 容器（Linux Containers，缩写为 LXC）。 Linux 容器不是模拟一个完整的操作系统，而是对进程进行隔离。有了容器，就可以将软件运行所需的所有资源打包到一个隔离的容器中。容器与虚拟机不同，不需要捆绑一整套操作系统，只需要软件工作所需的库资源和设置。系统因此而变得高效轻量并保证部署在任何环境中的软件都能始终如一地运行。
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525140222.png#crop=0&crop=0&crop=1&crop=1&id=rxTJs&originHeight=474&originWidth=340&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=) 

比较 Docker 和传统虚拟化方式的不同之处：

-  传统虚拟机技术是虚拟出一套硬件后，在其上运行一个完整操作系统，在该系统上再运行所需应用进程； 
-  而容器内的应用进程直接运行于宿主的内核，容器内没有自己的内核，而且也没有进行硬件虚拟。因此容器要比传统虚拟机更为轻便。 
-  每个容器之间互相隔离，每个容器有自己的文件系统 ，容器之间进程不会相互影响，能区分计算资源。 

# 5 Docker的优势

1.  更快速的应用交付和部署
传统的应用开发完成后，需要提供一堆安装程序和配置说明文档，安装部署后需根据配置文档进行繁杂的配置才能正常运行。Docker化之后只需要交付少量容器镜像文件，在正式生产环境加载镜像并运行即可，应用安装配置在镜像里已经内置好，大大节省部署配置和测试验证时间。 
2.  更便捷的升级和扩缩容
随着微服务架构和Docker的发展，大量的应用会通过微服务方式架构，应用的开发构建将变成搭乐高积木一样，每个Docker容器将变成一块“积木”，应用的升级将变得非常容易。当现有的容器不足以支撑业务处理时，可通过镜像运行新的容器进行快速扩容，使应用系统的扩容从原先的天级变成分钟级甚至秒级。 
3.  更简单的系统运维
应用容器化运行后，生产环境运行的应用可与开发、测试环境的应用高度一致，容器会将应用程序相关的环境和状态完全封装起来，不会因为底层基础架构和操作系统的不一致性给应用带来影响，产生新的BUG。当出现程序异常时，也可以通过测试环境的相同容器进行快速定位和修复。 
4.  更高效的计算资源利用
Docker是内核级虚拟化，其不像传统的虚拟化技术一样需要额外的Hypervisor支持，所以在一台物理机上可以运行很多个容器实例，可大大提升物理服务器的CPU和内存的利用率。 
