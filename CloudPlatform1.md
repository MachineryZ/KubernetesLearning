参考资料：https://www.bilibili.com/video/BV13Q4y1C7hS/?p=4&spm_id_from=pageDriver&vd_source=8635806d840eebcb9ee311685fcbaeaf 

# 云平台

1. 公有云
   1. 成本更低（前期）
   2. 无需维护
   3. 几乎无限制的缩放性（可多可少，根据业务来，不会溢出资源）
   4. 高可靠性
2. 购买机房，建立私有云
   1. 灵活性强，满足特定业务需求
   2. 控制力强，资源不与其他组织共享，有更高的隐私级别
   3. 可伸缩性（与本地相比，不如公有云）
3. 为什么“云”
   1. 环境统一
   2. 按需付费
   3. 即开即用
   4. 稳定性强
4. 国内常见云平台，阿里云、腾讯云、华为云、百度云、青云；国外常用云平台，亚马逊 AWS，微软 Azure

---

阿里云申请云平台资源 + 安装

Nginx：

- 高性能的 HTTP 和 反向代理 Web 服务器
  - 正向代理是代理客户端，让你正常访问目的服务器（A无法访问 google，但是 hk 服务器可以，于是 A 访问了hk 代理服务器）
  - 反向代理是代理服务器，让大量的请求均衡的访问到某一台服务器上（10w A 同时访问 google，反向代理服务器让 1w 访问 服务器B，1w 访问服务器 B等等，然后负载均衡）

云服务器 IP：

- 公网 ip：外部链接用
- 私有 ip：固定不变；集群内部用私有 ip 访问 
- VPC：私有网络、专有网络（virtual private cloud）提供逻辑隔离的虚拟网络环境
- 子网计算：ip 地址是十进制表示8位二进制；掩码部分，192.168.0.0/16 表示：后面有16位掩码，有效ip是 192.168.0.0 - 192.168.255.255 有 65536 个 可用 ip 个数
- 交换机是 192.168.0.0/24 （是前24不能变），是256个可用地址；另外的交换机：192.168.0.1/24，192.168.0.2/24，...，以此类推

---

Docker 概念：

1. docker 统一标准：应用构建（比如 c++，java）需要打成软件包。使用 docker build 打成标准的格式的包（镜像）
2. 应用分享：所有软件的镜像，可以放到一个指定地方 docker hub（很像 apple store，android app）
3. 应用运行：docker run 即可
4. docker 开启了 容器化时代
5. 对比 虚拟机技术
   1. 基础镜像 MB 级别
   2. 创建简单
   3. 隔离性强
   4. 启动速度秒级
   5. 移植和分享方便
6. 容器是：一个软件能够运行的最小级别单位

虚拟化技术：

1. 如果在真实机里面有内存泄漏，全部内存都会出现问题。
2. 虚拟机的出现可以解决资源隔离问题，但是有很多问题
   1. 虚拟机问题：
   2. 基础镜像 GB 级别，太大了
   3. 启动慢
   4. 移植和分享非常麻烦

架构：

1. docker host：安装 docker 的主机
2. docker daemon：运行在 docker 主机上的 docker 后台进程
3. client：操作 docker 主机的客户端（命令行、ui等）
4. registry：镜像仓库、docker hub
5. images：镜像、带环境打包好的程序，可以直接启动运行
6. containers：容器，由镜像启动起来正在运行中的程序

安装 docker：

1. https://docs.docker.com/desktop/install/linux-install/
2. 移除以前 docker 相关包
3. 配置 yum 源
4. 安装 docker；docker ce 社区版；docker ce cli 操作服务器的指令；containerd.io 容器运行环境
5. 开机启动

实战：

hub.docker.com 是docker hub 仓库找镜像

~~~shell
docker pull nginx # newest version
docker pull nginx:1.20.1
docker pull redis # newest version
docker pull reids:6.2.4
# download image into local
docker image # get images, repository tag imageid created size
docker rmi redis = docker rmi redis:latest
docker rmi image_id
~~~

启动容器：

~~~shell
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
docker run --name=mynginx nginx
~~~

停止容器

~~~shell
docker rm mynginx
docker rm 86567389012e

docker stop
docker start
docker restart
~~~



































