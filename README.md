# Docker基础核心技术笔记（立足于javaee）
  为什么学习？  自己正在奋力学习大数据，而大数据太多框架需要安装，所以为避免不必要的麻烦，学习一下Docker。

## 为什么会有Docker的出现？
由于开发+运维之间的协作出现的配置和环境问题。

## 解决方案：
开发端将代码、配置、系统、数据...全部打包。  
运维端利用Docker直接"复印"一份完全一样的
## Docker原理图
![image](image/Docker.png)

之前在服务器配置一个应用的运行环境，要安装各种软件，Java/Tomcat/MySQL/JDBC驱动包等 。
  安装和配置这些东西有多麻烦就不说了，它还不能跨平台。假如我们是在Windows上安装的这
    些环境，到了Linux又得重新装。况且就算不跨操作系统，换另一台同样操作系统的服务器，
      要移植应用也是非常麻烦的。  I

 传统上认为，软件编码开发/测试结束后，所产出的成果即是程序或是能够编译执行的二进制字
   节码等(java为例)。而为了让这些程序可以顺利执行，开发团队也得准备完整的部署文件，让
   维运团队得以部署应用程式，开发需要清楚的告诉运维部署团队，用的全部配置文件+所有软件
   环境。不过，即便如此，仍然常常发生部署失败的状况。Docker镜 像的设计，使得Docker得以
   打破过去「程序即应用」的观念。透过镜像(images)将作业系统核心除外，运作应用程式所需
   要的系统环境，由下而上打包，达到应用程式跨平台间的无缝接轨运作。

## Docker理念
Docker是基于Go语言实现的云开源项目。  
Docker的主要目标是“Build, Ship and Run Any App,Anywhere"，也就是通过对应用组件的封装、分发、部署、运行等生命周期的管理，使用户的APP (可以是一个WEB应用或数据库应用等等)及其运行环境能够做到“一次封装，到处运行”。    
![image](image/liniantu.PNG)   
Linux容器技术的出现就解决了这样-一个问题，而Docker就是在它的基础上发展过来的。将应用运行在Docker容器上面，而Docker容器在任何操作系统上都是一致的，这就实现了跨平台、跨服务器。只需要一次配置好环境，换到别的机子上就可以一-键部署好，大大简化了操作。

## Docker是什么？
解决了运行环境和配置问题软件容器，方便做持续集成并有助于整体发布的容器虚拟化技术。

## Docker能干什么？
### 之前的虚拟机技术
虚拟机(virtual machine)就是带环境安装的一种解决方案。  
它可以在种操作系统里面运行另一种操作系统，比如在Windows系统里面运行Linux 系统。应用程序对此毫无感知，因为虚拟机看上去跟真实系统一模-样，而对于底层系统来说，虚拟机就是一个普通文件，不需要了就删掉，对其他部分毫无影响。这类虚拟机完美的运行了另一套系统，能够使应用程序，操作系统和硬件三者之间的逻辑不变。  
![image](image/xuniji.png)

### 虚拟机的缺点
1.资源占用多 2.冗余步骤多 3.启动慢  

### 容器虚拟化技术
由于前面虚拟机存在这些缺点，Linux 发展出了另一种虚拟化技术: Linux 容器(Linux Containers,缩写为LXC)。  
Linux容器不是模拟一个完整的操作系统，而是对进程进行隔离。有了容器，就可以将软件运行所需的所有资源打包到一个隔离的容器中。容器与虚拟机不同，不需要捆绑一整套操作系统，只需要软件工作所需的库资源和设置。系统因此而变得高效轻量并保证部署在任何环境中的软件都能始终如一地运行。  
![image](image/Docker虚拟机.png)

比较了Docker和传统虚拟化方式的不同之处：  
* 传统虚拟机技术是虚拟出一套硬件后，在其上运行一个完整的操作系统，在该系统上再运行所需应用进程。  
* 而容器内的应用进程直接运行于宿主内核，容器内没有自己的内核，而且也没有进行硬件模拟。因此容器要比传统虚拟机更为轻便。  
* 每个进程之间相互隔离，每个容器有自己的文件系统，容器之间进程不会相互影响，能区分计算资源。这样耦合度进行低。  


### 开发/运维
一次构建，随处运维。  
1.更快速的应用交付和部署。  
2.更便捷的升级和扩缩容。  
3.更简单的系统运维。  
4.更高效的计算资源利用。  

### 企业
1.新浪 2.美团 3.....


### Docker的安装
## 前提说明：
Centos Docker安装
Docker支持一下的Centos版本：
Centos 7（64-bit）
Centos 6.5（64-bit）或者更高版本

## 前提条件
目前，CentOS仅发行版中的内核支持Docker。
Docker运行在CentOS 7上，要求系统为64位、系统内核版本为3.10以上。
Docker运行在CentOS-6.5或更高的版本的CentOS上，要求系统为64位、系统内核版本为2.6.32-431或者更高版本。

I
## 查看自己的内核
uname命令用于打印当前系统相关信息(内核版本号、硬件架构、主机名称和操作系统类型等)。
![image](image/内核.png)

## 查看已安装的CentOS版本信息
![image](image/版本信息.png)

Docker的基本组成
# Docker架构图
![image](image/Docker架构图.PNG)
# 1.镜像
镜像/容器
```
Person p1=new Person();
Person p2=new Person();
Person p3=new Person();
```
Docker镜像（Image）就是一个只读的模板。镜像可以用来创建Docker容器，一个镜像可以创建很多容器。
![image](image/镜像.PNG)
# 2.容器
Docker利用容器（Container）独立运行的一个或一组应用。容器是镜像创建的运行实例。
它可以被启动、开始、停止、删除。每个容器都是相互隔离的、保证安全的平台。
可以把容器看做是一一个简易版的Linux环境(包括root用户权限、进程空间、用户空间和网络空间等)和运行在其中的应用程序。
容器的定义和镜像几乎一模一样，也是一堆层的统一视角， 唯一区别在于容器的最上面那一层是可读可写的。





# 3.仓库

# 4.小总结



### Docker命令
## docker 常用命令如下
# 管理命令：
```
  container   管理容器
  image       管理镜像
  network     管理网络
  node        管理Swarm节点
  plugin      管理插件
  secret      管理Docker secrets
  service     管理服务
  stack       管理Docker stacks
  swarm       管理Swarm集群
  system      查看系统信息
  volume      管理卷
  
  如：docker container ls 显示所有容器
  ```
# 普通命令：
```
    
  attach     进入一个运行的容器
  build      从一个DockerFile构建镜像
  commit     从容器创建一个镜像
  cp          从容器和主机文件系统之间拷贝文件 
  create      创建一个容器
  diff        检查容器文件系统上的更改
  events      从服务器获取实时事件
  exec        在正在运行的容器中运行命令
  export      将容器的文件系统导出为tar存档
  history     显示镜像的历史记录
  images      查看镜像列表
  import      从归档文件中创建镜像
  info        显示系统范围的信息
  inspect     返回Docker对象的低级信息
  kill        kill运行中的容器
  load        从存档或者STDIN加载镜像
  login       登陆docker镜像仓库
  logout      退出docker镜像仓库
  logs        获取一个容器的日志
  pause       暂停一个或多个容器中的所有进程
  port        查看端口映射或容器的特定映射列表
  ps          查看容器列表
  pull        从镜像仓库拉取镜像
  push        将本地的镜像上传到镜像仓库,要先登陆到镜像仓库
  rename      重命名容器
  restart     重启容器
  rm          删除容器
  rmi         删除镜像
  run         创建一个新的容器并运行一个命令
  save        将指定镜像保存成 tar 归档文件
  search      从Docker Hub搜索镜像
  start       启动容器
  stats       实时显示容器资源使用情况的统计信息
  stop       停止容器
  tag         标记本地镜像，将其归入某一仓库
  top         展示一个容器中运行的进程
  unpause     恢复容器中所有的进程
  update      更新容器配置
  version    显示Docker的版本信息
  wait        阻塞直到容器停止，然后打印退出代码
  
  如：docker images 显示所有镜像

```
## 下面将分别介绍一些常用操作
# docker 拉取并运行一个镜像
1、下载镜像
`
$ docker pull centos
`  

2、查看已经下载的镜像
```
$ docker images
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    centos              latest              49f7960eb7e4        6 weeks ago         200MB
    hello-world         latest              f2a91732366c        8 months ago        1.85kB
```
3、运行一个镜像并生成容器
```
//运行一个centos镜像，并执行/bin/bash命令
$ docker run centos /bin/bash
```

输入命令docker ps或者docker container 

ls查看运行中的容器，发现列表为空，原因是容器在执行完成命令后会自动退出，下面介绍让让容器停留在后台的方法
```
$ docker ps
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    
$ docker container ls
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

使用命令docker ps -a或者docker container ls -a 查看所用容器,并显示了容器的状态
```
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
5525373371f3        centos              "/bin/bash"         7 minutes ago       Exited (0) 7 minutes ago                        nifty_rosalind
```

docker 让镜像运行停留在后台

1、启动一个容器并后台运行

docker run命令 通过增加-i -t参数可以让容器并进入容器
`
docker run -i -t centos /bin/bash
`

按 Ctrl + P + Q 退出容器，再用 docker ps 进行查看
```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
61b041e4e063        centos              "/bin/bash"         3 minutes ago       Up 3 minutes                            nervous_saha

```
状态显示仍在运行中

docker 进入一个运行的容器
```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
36afde543eb5        mysql:5.7           "docker-entrypoint.s…"   About an hour ago   Up About an hour    0.0.0.0:3306->3306/tcp   mymysql

$ docker exec -it 36afde543eb5 /bin/bash


-i 保持STDIN打开 -t 分配一个虚拟TTY窗口
```
docker 提交一个镜像到镜像仓库
1、首先到https://hub.docker.com/注册一个账号，保存下用户名密码 

2.控制台登陆dockerhub账户
```
$ docker login
    输入刚注册的用户名密码
```
2、查看镜像
```
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
redis               latest              f06a5773f01e        2 days ago          83.4MB
```

3、选择需要上传的镜像，重命名为指定的格式
`
$ docker  tag redis username/myredis:v1
`
username：为自己注册的用户名

myredis:为自己为镜像取的名字

v1：为任意设置的版本号

4、完成上述操作后，即可提交镜像到自己的仓库
`
docker push username/myredis:v1
`

docker 映射文件从宿主机到容器,端口号映射
//将宿主机的81端口映射到容器的80端口
//将宿主机的/develop/data卷，映射到容器的/data卷
```
$ docker run -i -t -p 81:80 -v /develop/data:/data  centos /bin/bash


-p:映射端口号 -v:磁盘目录映射
```

docker 更改端口号映射
运行中的容器无法映射新的端口号，也无法更改端口号映射，但可以通过两种方法解决

1、iptable转发端口
```
//查看容器ip
$ docker inspect 36afde543eb5 | grep IPAddress
"IPAddress": "172.17.0.2"

//将主机的8081端口映射到宿主机的8080端口
$ iptables -t nat -A  DOCKER -p tcp --dport 8081 -j DNAT --to-destination 172.17.0.2:8080
```

2、先提交容器为镜像，再运行这个容器，同时指定新的端口映射
```
//提交容器为镜像
$ docker commit 9995ffa15f46  mycentos:0.1
//停止旧的容器
$ docker stop 9995ffa15f46
//重新从旧的镜像启动容器
$ docker run -i -t  -p 8081:8080  mycentos:0.1


从DockerFile创建镜像
$ docker build -t myimage:v1 .
```
-t ：指定镜像名称和标签，格式为'name:tag' .: 最后一个点代表当前目录，也可以换成其它的路径