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
