# Dokcer

- [Dokcer](#dokcer)
  - [安装](#安装)
  - [Docker的常用命令](#docker的常用命令)
    - [1.帮助命令](#1帮助命令)
    - [2.镜像命令](#2镜像命令)
    - [3.docker search 搜索镜像](#3docker-search-搜索镜像)

## 安装

```shell
# 1.卸载旧版本
    yum remove docker \
    docker-client \
    docker-client-latest \
    docker-common \
    docker-latest \
    docker-latest-logrotate \
    docker-logrotate \
    docker-engine
# 2.需要的安装包
    yum install -y yum-utils

# 3.设置镜像的仓库
    # 默认是从国外的，不推荐
    yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

    # 推荐使用国内的
    yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
    
# 更新yum软件包索引
    yum makecache fast

# 4.安装docker相关的 docker-ce 社区版 而ee是企业版
    yum install docker-ce docker-ce-cli containerd.io # 这里我们使用社区版即可

# 5.启动docker
    systemctl start docker

# 6. 使用docker version查看是否按照成功
    docker version

# 7. 测试
    docker run hello-world
```

## Docker的常用命令

### 1.帮助命令

```shell
# 显示docker的版本信息。

docker version    
# 显示docker的系统信息，包括镜像和容器的数量

docker info       
# 帮助命令

docker 命令 --help 
```

### 2.镜像命令

```shell
# 查看所有本地主机上的镜像 可以使用docker image ls代替
docker images 

# 搜索镜像
docker search 

# 下载镜像 docker image pull
docker pull 

# 删除镜像 docker image rm
docker rmi 

# 查看所有本地的主机上的镜像
docker images 

# docker images
[root@iz2zeak7sgj6i7hrb2g862z ~] 
REPOSITORY            TAG                 IMAGE ID            CREATED           SIZE
hello-world           latest              bf756fb1ae65        4 months ago     13.3kB
mysql                 5.7                 b84d68d0a7db        6 days ago       448MB

# 说明
# 镜像的仓库源
  REPOSITORY 
# 镜像的标签(版本) ---lastest 表示最新版本
  TAG 
# ID 镜像的id
  IMAGE 
# 镜像的创建时间
  CREATED 
# 镜像的大小
  SIZE 

# 可选项
Options:
  # 列出所有镜像
  -a, --all         Show all images (default hides intermediate images) 
  # 只显示镜像的id
  -q, --quiet       Only show numeric IDs 
```

### 3.docker search 搜索镜像

```shell

# 列出所有镜像详细信息
[root@iz2zeak7sgj6i7hrb2g862z ~]# docker images -a  
# 列出所有镜像的id
[root@iz2zeak7sgj6i7hrb2g862z ~]# docker images -aq 

[root@iz2zeak7sgj6i7hrb2g862z ~]# docker search mysql

# docker search 搜索镜像

# --filter=STARS=3000 #过滤，搜索出来的镜像收藏STARS数量大于3000的
Options:
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results (default 25)
      --no-trunc        Don't truncate output
      
[root@iz2zeak7sgj6i7hrb2g862z ~]# docker search mysql --filter=STARS=3000

docker安装sql server

docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=Seclover1234!@#$' -p 1401:1433 --name sqlserver -d microsoft/mssql-server-linux 

docker rm $(docker ps -aq)

docker start $(docker ps -aq)

docker stop $(docker ps -aq)
```
