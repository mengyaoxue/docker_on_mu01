## 在现场集群安装及运行docker
在现场集群需使用 docker-rootless  
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


### 2.常用命令
docker ps -a
docker start a9d4bd5602e6
docker stop a9d4bd5602e6

https://www.cnblogs.com/linjiqin/p/8608975.html

$ docker kill a9d4bd5602e6
Error response from daemon: Cannot kill container: a9d4bd5602e6: Container a9d4bd5602e64942674a3f466501861c9dd8b63e2a5f1c774e37a007af56d688 is not running
