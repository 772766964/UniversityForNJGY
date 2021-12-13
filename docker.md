# Docker

## 命令

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

docker run 运行。。

+ --name：指定容器名称
+ -p：指定端口映射
+ -d：让容器后台运行

```
docker run --name my_nginx_2020 -d -p 80:80 --restart=always -e TZ="Asia/Shanghai" nginx:latest
```

docker stop my_nginx_2020

docker start my_nginx_2020

docker run --name containName 80:80 nginx



## 案例： Nginx

https://www.cnblogs.com/jying/p/12182715.html

### 步骤一：进入容器

`docker exec -it my_nginx_2020 bash`

### 命令解读：

docker exec ：进入容器内部执行命令

+ -it：给当前进入的容器一个标准输入输出的终端，允许我们与容器交互
+ my_nginx_2020：要进入的容器名称
+ bash：进入容器后执行的命令，bash是一个linux终端交互命令

## 案例：Redis容器，并执行redis-cli

https://www.cnblogs.com/ningy1009/p/12750416.html

### 命令解读

docker exec -it myredis bash

redis-cli



## linux 网卡配置修改（改成yes）

cd / 进入根目录 cd etc 进入etc目录 cd sysconfig 进入sysconfig目录 cd network-scripts 进入network-scripts vi ifcfg-ens33 编辑ifcfg-ens33文件 进入文件后执行如下操作: ①. 按 i 键 进入编辑状态 ②. 按↑↓键来移动光标, 删除no,输入yes ③. 按 ESC 键 ④. 输入 :wq ⑤. 按 ENTER 保存退出



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





# 完整的安装流程

https://www.icode9.com/content-3-1067574.html