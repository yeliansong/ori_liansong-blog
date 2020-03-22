---
layout:     post   		  # 使用的布局（不需要改）
title:      Understand The K8S Architecture    # 标题
subtitle:   学习笔记 #副标题
date:       2020-03-22 				# 时间
author:     Liansong 						# 作者
header-img: img/post-bg-desk.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - 学习笔记
    - tech
    - k8s
---

### 1. k8s components architecture.

![5555](https://tva1.sinaimg.cn/large/00831rSTgy1gd2v5xofmoj31iv0u0n7a.jpg)

Okay,  it's very easy to understand. Like above, master node is the most important. It controls the other nodes to join the cluster. Also API server is exposed outside. Through the master node, then can arrange the other nodes.

### 2. Practice

#### Target: Create the k8s cluster, then deploy the application to these 2 nodes.

#### Steps.

- Use kubeadm init to create the master k8s cluster, then join node1 and node2 to the cluster.

- In the master node, deploy the application with replications as 2.

  >ylsccnu1_gmail_com@liansong-instance:~$ kubectl run httpd-app --image=httpd --replicas=2
  >kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.
  >deployment.apps/httpd-app created

- After execute that, deployment is completed. You can execute command "kubectl get pods", show the deployment.

   >ylsccnu1_gmail_com@liansong-instance:~$ kubectl get pods -o wide
  >NAME               READY   STATUS    RESTARTS   AGE    IP  NODE NOMINATED NODE   READINESS GATES
  >httpd-app-c77bb8b47-pw848  1/1    Running        0  2m54s   10.244.2.2   liansong-instance-node1   
  >httpd-app-c77bb8b47-vz5f9   1/1     Running   0    2m54s   10.244.1.2   liansong-instance-node2   

  The application is deployed separately in the 2 nodes.  

### 3. Understand the process

![image-20200322182541280](https://tva1.sinaimg.cn/large/00831rSTgy1gd2vq6vm42j313s0u01co.jpg)

This is the whole process. 

When you execute "kubectl run", will call the API Server, then API Server notice the Controller Server to create the deployment resource. After that, Schedule service will arrange the tasks to the node1 and node2. In the node1 and node2, kubelet will create the pods according to the tasks. Kube-proxy will arrange the network config for these 2 nodes. 



