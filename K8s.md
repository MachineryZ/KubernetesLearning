# Kubernetes

https://www.yuque.com/leifengyang/oncloud/ctiwgo

K8s 是什么

1. 传统部署方式：多个 app 在同一个 operating system 中启动，一个 app 崩溃会导致同一个操作系统崩溃
2. 虚拟化部署方式：在物理机上，封装一个 virtual machine（虚拟机），在虚拟机里实现的 app；但是缺点是太笨拙了
3. 容器化部署：在 operating system 上封装 conatainer routime，以容器化的方式进行（仅需几十 mb）
4. 容器化部署的问题：如果有一个很大量的容器，某个容器崩溃，我们需要自动化的修复容器，需要一个大规模容器编排系统



Kubernetes 具有以下特性：

1. 服务发现和负载均衡。k8s 可以使用 dns 名称或自己的 ip 地址公开容器，如果进入容器的流量很大，k8s 可以负载均衡
2. 存储编排：k8s 允许你自动挂在你选择的存储系统，例如本地存储，公共云提供商等
3. 自动部署和回滚：你可以使用 k8s描述已部署容器所需状态，它可以以受控的速率将实际状态更改为期望状态。例如，你可以自动化 k8s 来为你的部署创建新容器，删除现有容器并将他们的所有资源用于容器。
4. 自动完成装箱计算：k8s 允许你指定每个容器和内存 RAM。当容器制定了资源请求时，k8s 可以做出更好的决策来管理容器的资源
5. 自我修复：k8s 重新启动失败的容器、替换容器杀不死响应用户定义的运行状况检查的容器，并且在准备好服务之前不将其通告给客户端
6.   例子，k8s 可以轻松管理系统的 canary 部署（金丝雀部署，**一种流行的持续部署策略，将小部分用户更新到您的应用程序的新版本**。 在采用持续交付时，公司需要决定使用哪种类型的部署策略。 最流行的策略之一是金丝雀部署，将小部分用户首先更新到新版本。 如果应用程序的新版本出现问题，只有一小部分用户会受到影响，并且可以修复或快速恢复更改）

架构

- k8s cluster = N master node + N Worker Node （master 节点 + worker 节点）
- 一些概念，api server; cloud controller; kubelet;kube-proxy;scheduler; control plane
- controller manage 决策者
- control plane 总部
- node 
- etcd 资料库
- api server 和 决策者对接，和资料库对接进行文件传输和存储
- Scheduler 调度者，负责和节点分配任务
- kubelet 是每个节点的管理者
- Kube-proxy 是和外界信息交流的代理

![ ](/Users/zhangzhizuo/Library/Application Support/typora-user-images/image-20240216134150480.png)

K8s 集群部署

- 安装 docker，kubelet，kubectl（对k8s的命令行），kubeadm（安装k8s的快速仓库），
- Master kubeadm init（安装各种 k8s 组件）
- worker node kubeadm join（加入当前 master 节点）

青云服务器的一些资源申请，然后进行小 project ；申请 3 node，master 节点一个，剩下两个是 worker node。内网穿透（什么是内网穿透？ 内网穿透，简单地说就是**内网的数据让外网可以获取，可以映射到公共网络上，这样就可以在公共网络上访问内网的数据**。 内网是不能被外网直接访问的，只能通过一些中转技术，如DingTalk Design CLI、花生壳、Natap 等工具，让内网“假装”成外网，就是内网穿透。） 

---

实战

Kubernetes 集群部署 

- 配置 yum 源
- 配置 yum
- 安装 docker
- 启动 docker
- selinux 设置为   permissive 模式
- 关闭 swap 
- 安装 kubelet、kubeadm、kubectl

~~~bash
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=http://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
   http://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
exclude=kubelet kubeadm kubectl
EOF


sudo yum install -y kubelet-1.20.9 kubeadm-1.20.9 kubectl-1.20.9 --disableexcludes=kubernetes

sudo systemctl enable --now kubelet
~~~

- 初始化 master 节点
- 增加网络插件
- 加入 node 节点
- 验证集群，查看集群部署了哪些应用（运行中的应用在 docker 里面叫容器，在 k8s 里面叫 pod
- 部署 dashboard
- 等待 nodes 节点全部 ready 然后开始跑命令
- 全部命令需要在 master 节点上进行
- 集群自修复能力
- 设置访问端口
- 

















