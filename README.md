## 在现场集群安装及运行docker
在现场集群需使用 docker-rootless  
并交互式调用一计算节点
`qsub -I -q cu_slim`

### 1.安装
参考 https://docs.docker.com/engine/security/rootless/#install  

```
$ curl -fsSL https://get.docker.com/rootless >> get_docker.sh
```
由于现场连外网速度非常慢，故需要修改生成的 get_docker.sh 将下载路径改为国内镜像地址（这里以科大镜像源为例）。  
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
首先需要交互式调用一计算节点，然后用以下命令启动docker服务
```
dockerd-rootless.sh --experimental --storage-driver vfs
```
再新开一个交互式计算节点，在里面使用docker

常用命令
```
docker ps -a
docker start a9d4bd5602e6
docker stop a9d4bd5602e6
docker kill a9d4bd5602e6  
Error response from daemon: Cannot kill container: a9d4bd5602e6: Container a9d4bd5602e64942674a3f466501861c9dd8b63e2a5f1c774e37a007af56d688 is not running
```
https://www.cnblogs.com/linjiqin/p/8608975.html

`docker image load` 
```
docker image load -i /home/miaocc/pulsar-TIMING.img
```
可参考  
https://docs.docker.com/engine/reference/commandline/image_load/


