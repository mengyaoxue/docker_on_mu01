## 在现场集群安装及运行docker
在现场集群需使用 docker-rootless  
并交互式调用一计算节点
`qsub -I -q cu_slim`

### 1.安装
参考 https://docs.docker.com/engine/security/rootless/#install  

```
$ curl -fsSL https://get.docker.com/rootless >> get_docker.sh
```
由于现场集群连国外网受限速度非常慢，故需要修改生成的 get_docker.sh 将下载路径改为国内镜像地址（这里以科大镜像源为例）。  
将生成的 `get_docker.sh` 中
```
        STATIC_RELEASE_URL="https://download.docker.com/linux/static/$CHANNEL/$(uname -m)/docker-${STABLE_LATEST}.tgz"
        STATIC_RELEASE_ROOTLESS_URL="https://download.docker.com/linux/static/$CHANNEL/$(uname -m)/docker-rootless-extras-${STABLE_LATEST}.tgz"
```
改为
```
        STATIC_RELEASE_URL="https://mirrors.ustc.edu.cn/docker-ce/linux/static/$CHANNEL/$(uname -m)/docker-${STABLE_LATEST}.tgz"
        STATIC_RELEASE_ROOTLESS_URL="https://mirrors.ustc.edu.cn/docker-ce/linux/static/$CHANNEL/$(uname -m)/docker-rootless-extras-${STABLE_LATEST}.tgz"
```
运行
```
$ bash get_docker.sh
```
一切顺利的话会看得到如下屏幕输出


TODO  


### 2.运行
首先需要交互式调用一**计算节点**，
```
qsub -I -q cu_slim
```

然后用以下命令启动docker服务
```
dockerd-rootless.sh --experimental --storage-driver vfs
```
再新开一个交互式计算节点，在里面使用docker  
可尝试
```
docker run hello-world
```


常用命令
```
docker ps -a
docker start a9d4bd5602e6
docker stop a9d4bd5602e6
docker kill a9d4bd5602e6  
Error response from daemon: Cannot kill container: a9d4bd5602e6: Container a9d4bd5602e64942674a3f466501861c9dd8b63e2a5f1c774e37a007af56d688 is not running
```

```
docker images
```
https://www.cnblogs.com/linjiqin/p/8608975.html

docker image load   
(可参考 https://docs.docker.com/engine/reference/commandline/image_load/)

具体所使用的命令:
```
docker image load -i /home/miaocc/pulsar-TIMING.img
```
经过 **6!个!小!时!** 的镜像加载(MD从下午3点半一直搞到晚上9点半),终于显示  
```
Loaded image: fast_psr:timing
```
然后
```
docker images
```
的时候就可以看到有列出 fast_psr 了


### 3.Run Docker-service in screen  
(https://www.cnblogs.com/mchina/archive/2013/01/30/2880680.html)  

(http://www.dayid.org/comp/tm.html)

开启screen `screen`  

显示已有screen列表 `screen -ls`  

临时退出session `Ctrl+a d`  

在session中翻页
>Ctrl+a \[  

退出翻页模式: `Ctrl+c`

创建指定名称的session
>screen -S $session_name

进入已存在的session
>screen -r $session_name

删除指定session
>screen -X -S $session_name quit

删除当前session: `Ctrl+a k`  

For dead sessions use: `screen -wipe`



### TODO
PINT not TEMPO3
https://nanograv-pint.readthedocs.io/en/latest/

