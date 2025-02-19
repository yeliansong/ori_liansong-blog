---
layout:     post   				    # 使用的布局（不需要改）
title:      一：Kubernetes的介绍 				# 标题
subtitle:   Kubernetes in action 读书笔记 #副标题
date:       2019-09-10 				# 时间
author:     Liansong 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - 读书笔记
    - tech
    - k8s
    - docker
---

### 1. 单体应用和微服务的比较   

单体应用的弊端：以单进程或几个进程的方式运行于几台服务器，部署的周期长，运维和开发脱节，开发人员完成开发后打包成一个整体给运维部署。   

模块间没有解耦，修改一个模块，要把整体进行打包部署。   

微服务的优势：模块间实现解耦，缩短部署周期，单个模块可以实现独立的开发，部署，升级，伸缩。缩短部署时间。还有节约资源，模块间可以单独
 的进行扩容，而不用扩容所有。



### 2. DevOps 

微服务带来了DevOps。 以前的团队组合是，开发人员完成开发后把成果物给运维，然后运维完成部署，开发和运维是完全分开的。这就带来一个问题，开发人员不能第一时间了解用户的需求，而且也不了解系统的运行环境，而运维也不了解产品的功能。微服务来了后，通过kubernetes对系统硬件资源的虚拟化，使开发人员不用担心部署环境，简化系统的部署，开发人员也可以参与到部署中，也就衍生了DevOps。


### 3. 容器技术

容器技术其实就是Linux的隔离技术。通过什么来进行隔离呢？ 命名空间和CGROUP。 命名空间是用来隔离不同的进程，CGROUP是用来隔离资源。就是通过这个能够使一个宿主机可以运行多个不同的应用程序。同一个宿主机上的两个应用程序也可以共享文件，如果共用同一个基本镜像，就是共用资源，但是 这一层文件是只读的，如果重写写入，是在基本镜像基础上写入一层文件，容器是用的联合文件系统。

<img src="https://cdn.jsdelivr.net/gh/yeliansong/github-blog-PIC/blog-images006y8mN6gy1g6ur4b89noj30f708qq5w.jpg" style="zoom:200%;" />

<img src="https://cdn.jsdelivr.net/gh/yeliansong/github-blog-PIC/blog-images006y8mN6gy1g6ur7hcbvdj309f0h5n02.jpg" style="zoom:200%;" />

### 4. 容器的移植

容器的镜像是一个完整的系统，经过裁减后的。它裁减的还是宿主机的，所以一个容器镜像能否运行还是要看镜像所在运行的环境。如果编排镜像的宿主机环境的内核版本和运行环境一致，则可以运行。同时也要看是否用到宿主机特有的一些系统资源。



### 5. Kubernetes

Google搞出这个东西，是为了解决Google成千上万服务器的管理部署问题。之后容器技术火后，Kubernetes对容器的支持，所以说也可以说是Kubernetes成就了Docker。相符相承吧。Kubernetes的设计宗旨是将底层基础设施进行抽象化，通过给你提供一个主节点，来管理成千上万的你的服务的运行节点。你不用 关心你的服务运行节点的部署。

<img src="https://cdn.jsdelivr.net/gh/yeliansong/github-blog-PIC/blog-images006y8mN6gy1g6ur4cniqdj30eg05lac3.jpg" style="zoom:150%;" />



### 6. Kubernetes 的组成

主节点： API服务器（功能入口，管理其他模块）， Schedule（调度应用）， Control Manager， etcd（分布式数据存储）   

工作节点： kubelet (与API进行通信，管理容器)， kube-proxy(负责网络流量均衡)

<img src="https://cdn.jsdelivr.net/gh/yeliansong/github-blog-PIC/blog-images006y8mN6gy1g6ur7idxf5j30ey05xgo0.jpg" style="zoom:150%;" />
