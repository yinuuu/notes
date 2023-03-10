---
title: Docker 常用命令
author: yinuuu
date: 2023-2-19
categories:
  - Tools
tags:
  - Docker
sticky: 1
---

### 1 帮助命令
####  1.1 docker version
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525150924.png#crop=0&crop=0&crop=1&crop=1&id=zZZA6&originHeight=693&originWidth=741&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
####  1.2 docker info
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525151007.png#crop=0&crop=0&crop=1&crop=1&id=ryvWC&originHeight=1056&originWidth=1028&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
#### 1.3 docker --help(-h)
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525151103.png#crop=0&crop=0&crop=1&crop=1&id=gCvrY&originHeight=1056&originWidth=1761&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
### 2 镜像命令
#### 2.1 docker images 列出本地主机上的镜像
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525152014.png#crop=0&crop=0&crop=1&crop=1&id=SB8l0&originHeight=127&originWidth=1070&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

   -  REPOSITORY：表示镜像的仓库源 
   -  TAG：镜像的标签 
   -  IMAGE ID：镜像ID 
   -  CREATED：镜像创建时间 
   -  SIZE：镜像大小
同一仓库源可以有多个 TAG，代表这个仓库源的不同个版本，我们使用 REPOSITORY:TAG 来定义不同的镜像。 如果你不指定一个镜像的版本标签，例如你只使用 ubuntu，docker 将默认使用 ubuntu:latest 镜像 
   -  images 命令 的 option 参数 
      -  -a:列出本地所有的镜像（含中间映像层） 
      -  -q :只显示镜像ID
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525152339.png#crop=0&crop=0&crop=1&crop=1&id=I2H3n&originHeight=77&originWidth=618&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=) 
      -  --digests :显示镜像的摘要信息
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525152552.png#crop=0&crop=0&crop=1&crop=1&id=oW2ui&originHeight=177&originWidth=1881&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=) 
      -  --no-trunc :显示完整的镜像信息
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525152638.png#crop=0&crop=0&crop=1&crop=1&id=aZa7G&originHeight=171&originWidth=1884&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
#### 2.2 docker search 镜像名          
 从 Docker hub 官网搜索镜像以 tomcat 为例
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525152813.png#crop=0&crop=0&crop=1&crop=1&id=SjHf3&originHeight=675&originWidth=1536&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
和在官网搜索的结果一模一样
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525152954.png#crop=0&crop=0&crop=1&crop=1&id=RePhi&originHeight=963&originWidth=1883&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

-  参数说明 
   -  -s : 列出收藏数不小于指定值的镜像
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525153109.png#crop=0&crop=0&crop=1&crop=1&id=JkRTq&originHeight=174&originWidth=1432&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
只搜索点赞数大于30的镜像 
   -  --no-trunc : 显示完整的镜像描述 
   -  --automated : 只列出 automated build类型的镜像 
#### 2.3 docker pull 镜像名:tag     
拉取镜像(从前面我们已经设置的阿里云的镜像加速地址)
	如果 `docker pull 镜像名` 后面不加参数,默认下载最新版本
	即 docker pull tomcat 等价于 docker pull tomcat:latest 
```shell
docker pull tomcat
```

![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525153705.png#crop=0&crop=0&crop=1&crop=1&id=klhL3&originHeight=395&originWidth=961&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525153806.png#crop=0&crop=0&crop=1&crop=1&id=zS6Gr&originHeight=128&originWidth=1063&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
#### 2.4 docker rmi 镜像名/镜像id 
删除 Docker 镜像
	ps: `docker rmi 镜像名` 默认会删除标签为 :latest 的镜像,如果要删除指定标签的镜像,在镜像名后面指定 tag 即可
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525153922.png#crop=0&crop=0&crop=1&crop=1&id=H3MMz&originHeight=69&originWidth=1873&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
如果无法删除,出现如上提示,表示我们的镜像正在使用中,可以使用 -f 强制删除
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200525153954.png#crop=0&crop=0&crop=1&crop=1&id=F637M&originHeight=98&originWidth=1194&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
如果想要删除多个镜像
	docker rmi -f 镜像名1:tag 镜像名2:tag 
```shell
sudo docker rmi -f hello-world tomcat
```
删除全部镜像 
```yaml
sudo docker rmi -f $(docker images -qa)
```
#### 2.5 镜像重命名
```shell
docker image tag test:latest my_docker/test:latest
docker image tag fb583c3ac45d  my_docker/test:latest
```
### 3 容器命令
####  3.1 docker pull 下载容器
以 CentOS 为例,从阿里云下载一个 CentOS 的镜像
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526090859.png#crop=0&crop=0&crop=1&crop=1&id=LeMfq&originHeight=272&originWidth=1047&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
####  3.2 docker run 新建并启动容器
```shell
docker run [options] image [command] [arg...]
```
options 这里常用的有:
--name="容器新名字": 为容器指定一个名称； -d: 后台运行容器，并返回容器ID，也即启动守护式容器； -i：以交互模式运行容器，通常与 -t 同时使用； -t：为容器重新分配一个伪输入终端，通常与 -i 同时使用； -P: 随机端口映射； -p: 指定端口映射，有以下四种格式
`1.ip:hostPort:containerPort 2.ip::containerPort 3.hostPort:containerPort 4.containerPort`
我们使用 -it 参数来启动 CentOS 容器
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526092354.png#crop=0&crop=0&crop=1&crop=1&id=FaXXP&originHeight=141&originWidth=1368&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
root@ 后面跟着的就是该容器的 id 
#### 3.3 docker ps 查看所有运行的容器命令
docker ps [options]
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526092457.png#crop=0&crop=0&crop=1&crop=1&id=qfzkV&originHeight=80&originWidth=1586&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
参数说明:
-a :列出当前所有正在运行的容器+历史上运行过的容器 -l :显示最近运行的容器。 -n number：显示最近 number 个创建的容器。 -q :静默模式，只显示容器编号。 --no-trunc :不截断输出。 
#### 3.4 exit 退出容器
```
exit: 容器停止并退出
ctrl+p+q: 容器不停止退出
```
#### 3.5 docker start 启动已经创建的容器
```
docker start 容器id/容器名
```
#### 3.6 docker restart 重启容器
```
docker restart 容器id/容器名
```
#### 3.7 docker stop 停止容器
```
docker stop 容器id/容器名
```
#### 3.8 docker kill 强制关闭容器
```
docker kill 容器id/容器名
```
#### 3.9 docker rm 删除已停止的容器
```
docker rm 容器id/容器名

一次性删除多个已经停止的容器
docker rm -f $(docker ps -qa) 或者 docker ps -a -q | xargs docker rm
```
#### 3.10 交互式容器和守护式容器
前面启动 CentOS 容器使用的 -it 参数就是表示交互式命令,通过终端来保持和容器的交互
如果要启动守护式容器,那么需要加上 -d 参数
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526093221.png#crop=0&crop=0&crop=1&crop=1&id=NcXIB&originHeight=126&originWidth=1535&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
但是此时查询正在运行的容器，没有发现以后台模式运行的 Docker 容器
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526093331.png#crop=0&crop=0&crop=1&crop=1&id=BoRYZ&originHeight=101&originWidth=1723&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
发现该容器已经自动退出了 
> 问题：docker ps -a 进行查看, 会发现容器已经退出 很重要的一点: Docker容器后台运行,就必须有一个前台进程. 容器运行的命令如果不是那些一直挂起的命令（比如运行top，tail），是会自动退出的。
>  
> 这个是docker的机制问题,比如你的web容器,我们以nginx为例，正常情况下,我们配置启动服务只需要启动响应的service即可。例如 service nginx start 但是,这样做,nginx为后台进程模式运行,就导致docker前台没有运行的应用, 这样的容器后台启动后,会立即自杀因为他觉得他没事可做了. 所以，最佳的解决方案是,将你要运行的程序以前台进程的形式运行

#### 3.11 docker logs 容器日志
```shell
// 对于后台运行的容器,可以以下面的方式来启动 
docker run -d --name centos02 centos /bin/sh -c "while true;do echo hello world;sleep 2;done"
```

![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526093745.png#crop=0&crop=0&crop=1&crop=1&id=XnZZf&originHeight=209&originWidth=1605&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
即便是后台启动,但是因为前台一直打印日志,Docker 容器也不会自动关闭
如果此时我们想去查看 Docker 容器的日志,可以通过以下命令
```
docker logs -f -t --tail 容器ID/容器名
```

-  -t 是加入时间戳 
-  -f 跟随最新的日志打印 
-  --tail 数字 显示最后多少条
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526094051.png#crop=0&crop=0&crop=1&crop=1&id=PxGAA&originHeight=430&originWidth=857&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
#### 3.12 docker top 查看容器内运行的进程
```
docker top 容器ID/容器名
```

![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526094217.png#crop=0&crop=0&crop=1&crop=1&id=HJ4B6&originHeight=152&originWidth=1881&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
#### 3.13 docker inspect 查看容器内部细节
```
docker：如何查看容器的挂载目录
docker inspect container_name | grep Mounts -A 20
docker inspect container_id | grep Mounts -A 20
```

![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526094333.png#crop=0&crop=0&crop=1&crop=1&id=uvdeI&originHeight=1071&originWidth=1191&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
#### 3.14 进入正在运行的容器并以命令行交互
重新进入正在运行的容器 
```shell
docker attach 容器ID/容器名
```
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526094831.png#crop=0&crop=0&crop=1&crop=1&id=nvby2&originHeight=120&originWidth=1322&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
还有一种方式是
```
docker exec -it 容器ID/容器名 bash(功能更加强大,可以直接返回结果到客户端)
```

- **-i**: 交互式操作。
- **-t**: 终端。
- **/bin/bash**：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。

区别在于:

-  attach 命令直接进入容器启动命令的终端，不会启动新的进程 
-  exec 命令是在容器中打开新的终端，并且可以启动新的进程 
#### 3.15 docker cp 从容器内拷贝文件到主机上
```
docker cp 容器ID(或容器名):容器内路径 目的主机路径
```
示例如下
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526095315.png#crop=0&crop=0&crop=1&crop=1&id=wLPn4&originHeight=203&originWidth=698&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
### 4 常用命令总结
![](https://gitee.com/krislin_zhao/IMGcloud/raw/master/img/20200526095411.png#crop=0&crop=0&crop=1&crop=1&id=IdqqK&originHeight=638&originWidth=900&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

```
attach    Attach to a running container                 # 当前 shell 下 attach 连接指定运行镜像

build     Build an image from a Dockerfile              # 通过 Dockerfile 定制镜像

commit    Create a new image from a container changes   # 提交当前容器为新的镜像

cp        Copy files/folders from the containers filesystem to the host path   #从容器中拷贝指定文件或者目录到宿主机中

create    Create a new container                        # 创建一个新的容器，同 run，但不启动容器

diff      Inspect changes on a container's filesystem   # 查看 docker 容器变化

events    Get real time events from the server          # 从 docker 服务获取容器实时事件

exec      Run a command in an existing container        # 在已存在的容器上运行命令

export    Stream the contents of a container as a tar archive   # 导出容器的内容流作为一个 tar 归档文件[对应 import ]

history   Show the history of an image                  # 展示一个镜像形成历史

images    List images                                   # 列出系统当前镜像

import    Create a new filesystem image from the contents of a tarball # 从tar包中的内容创建一个新的文件系统映像[对应export]

info      Display system-wide information               # 显示系统相关信息

inspect   Return low-level information on a container   # 查看容器详细信息

kill      Kill a running container                      # kill 指定 docker 容器

load      Load an image from a tar archive              # 从一个 tar 包中加载一个镜像[对应 save]

login     Register or Login to the docker registry server    # 注册或者登陆一个 docker 源服务器

logout    Log out from a Docker registry server          # 从当前 Docker registry 退出

logs      Fetch the logs of a container                 # 输出当前容器日志信息

port      Lookup the public-facing port which is NAT-ed to PRIVATE_PORT    # 查看映射端口对应的容器内部源端口

pause     Pause all processes within a container        # 暂停容器

ps        List containers                               # 列出容器列表

pull      Pull an image or a repository from the docker registry server   # 从docker镜像源服务器拉取指定镜像或者库镜像

push      Push an image or a repository to the docker registry server    # 推送指定镜像或者库镜像至docker源服务器

restart   Restart a running container                   # 重启运行的容器

rm        Remove one or more containers                 # 移除一个或者多个容器

rmi       Remove one or more images             # 移除一个或多个镜像[无容器使用该镜像才可删除，否则需删除相关容器才可继续或 -f 强制删除]

run       Run a command in a new container              # 创建一个新的容器并运行一个命令

save      Save an image to a tar archive                # 保存一个镜像为一个 tar 包[对应 

load]

search    Search for an image on the Docker Hub         # 在 docker hub 中搜索镜像

start     Start a stopped containers                    # 启动容器

stop      Stop a running containers                     # 停止容器

tag       Tag an image into a repository                # 给源中镜像打标签

top       Lookup the running processes of a container   # 查看容器中运行的进程信息

unpause   Unpause a paused container                    # 取消暂停容器

version   Show the docker version information           # 查看 docker 版本号

wait      Block until a container stops, then print its exit code   # 截取容器停止时的退出状态值
```
