# Docker



## Docker 安装



### linux 网卡配置修改（改成yes）

cd /etc/sysconfig/network-scripts

vi ifcfg-ens33

编辑ifcfg-ens33文件 进入文件后执行如下操作: 

①. 按 i 键 进入编辑状态

 ②. 按↑↓键来移动光标, 删除no,输入yes 

③. 按 ESC 键 

④. 输入 :wq 

⑤. 按 ENTER 保存退出



### 可以为docker设置yum源

```bash
yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

### 可以查看所有仓库中所有docker版本，并选择特定版本安装

```bash
yum list docker-ce --showduplicates | sort -r
```

### 安装docker

```bash
yum install docker-ce docker-ce-cli containerd.io
```

### 或者安装指定版本

```bash
yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
```

###  配置镜像加速

中国科学技术大学的开源镜像 https://docker.mirrors.ustc.edu.cn

网易的开源镜像： https://hub-mirror.c.163.com

### 创建与启动容器

```bash
docker run [options] IMAGE [command] [arg...]
```

- `-i` 表示运行容器
- `-t` 表示容器启动后进入其命令行。加入这两个参数后，容器创建就能登录进去。即分配一个伪终端
- `--name` 为创建的容器命名
- `-v`表示目录映射关系（前者是宿主机目录，后者是映射到宿主机上的目录），可以使用多个-v做多个目录或文件映射。
  注意：最好做目录映射，在宿主机上做修改，然后共享到容器上
- `-d` 在run后面加上-d参数，则会创建一个守护式容器在后台运行（这样创建容器后不会自动登录容器，如果只加`-i -t`两个参数，创建容器后就会自动进容器里）
- `-p` 表示端口映射，前者是宿主机端口，后者是容器内的映射端口，可以使用多个-p做多个端口映射
- `-P` 随机使用宿主机的可用端口与容器内暴露的端口映射

##### 5.2.2.1 创建并进入容器

```bash
docker run -it --name 容器名称 镜像名称:标签 /bin/bash
```

此命令表示： 通过镜像A创建容器B，运行并进入容器的`/bin/bash`

> 注意：docker 容器运行必须有一个前台进程，如果没有前台进程执行，容器认为是空闲状态，就会自动退出。



### Docker命令

systemctl start docker 启动

docker ‐v 版本

ps -ef|grep docker 

systemctl enable docker

systemctl stop docker

docker images  展示镜像

docker pull nginx  拉下来需要的镜像

docker search mysql 去搜索相关资源

docker save 导出镜像到磁盘

docker load 加载镜像

docker xx --help 可以查看xx的语法

docker exec 进入容器执行命令

docker logs 查看容器运行日志

+ -f: 持续查看日志

docker ps 查看容器运行状态

docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

+ --name：指定容器名称
+ -p：指定端口映射
+ -d：让容器后台运行


docker stop/stop my_nginx_2020

docker run --name containName 80:80 nginx





## 案例： Nginx

https://www.cnblogs.com/jying/p/12182715.html

### 步骤一：进入容器

```
docker run --name my_nginx -d -p 80:80 --restart=always -e TZ="Asia/Shanghai" nginx:latest
```

`docker exec -it my_nginx bash`

### 命令解读：

docker exec ：进入容器内部执行命令

+ -it：给当前进入的容器一个标准输入输出的终端，允许我们与容器交互
+ my_nginx：要进入的容器名称
+ bash：进入容器后执行的命令，bash是一个linux终端交互命令

## 案例：Redis容器，并执行redis-cli

https://www.cnblogs.com/ningy1009/p/12750416.html

### 命令解读

docker exec -it myredis bash

redis-cli







## 数据卷

https://blog.51cto.com/hongge/1844249

数据卷(volume)是一个虚拟目录，指向宿主机文件系统中的文件，不用再进入容器内修改。

### 作用

将容器与数据分离，解耦合，方便操作容器内数据，保证数据安全

### 数据卷操作

docker volume create

docker volume ls

docker volume  inspect

docker volume  rm

docker volume  prune

## 案例：创建一个数据卷

docker run 创建并运行容器

+ name mynginx 给容器起名mynginx
+ -v html:/root/html 把html数据卷挂载到容器内的/root/html目录
+ -p 8080:80 把宿主机的8080端口映射到容器内的80端口
+ nginx 镜像名称

步骤：

+ 创建容器并挂载数据卷到容器内的HTML目录

+ `docker run --name mynginx -v html:/usr/share/nginx/html -p 80:80 -d nginx`

+ 进入html数据卷所在位置，并修改HTML内容

+ ``` 
  # 创建数据卷
  cocker volume create html
  # 查看html数据卷位置
  docker volume inspect html
  # 进入该目录(在第一项完成后查看url)
  cd url
  # 修改文件
  vi index.html
  ```

+ 

### 数据卷挂载方式

+ -v volumeNmae:/targetContainerPath
+ 如果容器运行时bolume不存在，会自动被创建出来



## jar包

jar复制粘贴之后，需要下载解压的

yum install -y lrzsz



## Docker Compose

下载



## Docker 镜像仓库





## 遇到问题

### 权限不够？

chmod 777

chmod +x /地址  更改权限



## 作业2021年12月13日

时限：3点-5点

+ 安装mysql容器，给mysql挂在本地目录

  ​	将sql语句执行

+ 安装redis
+ 安装es，kibana
+ 完成docker-cpmpose的案例，部署微服务集群



# 完整的安装流程

https://www.icode9.com/content-3-1067574.html

