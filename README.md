# 小白教程：使用DOCKER运行多个Phala节点教程（复制捏贴就行）
声明我也是小白一枚，该教程其实就是我在Ubantu18.04上使用docker 搭建Phala 全节点的一个过程整理，
希望能做到尽量详细，让参考者直接拷贝黏贴命令就能轻松搭建Phala 全节点。

## 1. Docker 安装（已经安装过Docker 的跳过该步骤）

### 卸载旧版本

   sudo apt-get remove docker docker-engine docker.io containerd runc

### 一键安装
 
  curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun

### 测试 Docker 是否安装成功，输入以下指令

  sudo docker run hello-world

在打印的一堆信息中能找到以下信息则安装成功:

Hello from Docker!
This message shows that your installation appears to be working correctly.

手动安装可以参考以下链接：
Linux：https://www.runoob.com/docker/centos-docker-install.html 

## 2. 搭建全节点

### 先新建一个文件夹，并进入该文件夹
  
   mkdir phala-network    
   cd phala-network
   
### 下载节点应用，这个过程需要一个小时左右

   curl -sL https://github.com/Phala-Network/phala-blockchain/releases/download/poc2-3.0-alpha1/phala-node -o phala-node

### 新建一个Dockerfile

   touch Dockerfile

### 编辑该Dockerfile 如下并保存：

  FROM ubuntu:18.04  
  MAINTAINER name  
  WORKDIR  /home  
  COPY . .  
  RUN chmod +x phala-node  
  CMD ./phala-node --chain poc2 --name "youname | your phala address" 

### 创建docker 镜像(最后面的 . 不要漏了）

  docker build -t phala-node:phala .

### 运行docker 容器(yourname 跟phala地址改成你的，可以跑多个节点）

  docker run -d -it phala-node:phala --chain poc2 --name "yourname | 5EkeZ7hGq323fkdFKBANsLLdAnpnvkjpLrd494Msk6JqrGot"

### 到这里节点就搭建成功了，可以到telemtry去查看你的节点

https://telemetry.polkadot.io/#list/Phala%20PoC-2

也可以到这里查看节点运行了多少个eras

https://poc2-dashboard.phala.network/#/


题外话：我是在华为云服务器（2核4G）上操作的，疫情期间搞活动买的三年期，平均1块钱/天，感兴趣的
朋友可以去华为云官网了解。：
