# centos

- [centos](#centos)
  - [配置网卡](#配置网卡)
  - [配置yum源、安装依赖、升级依赖](#配置yum源安装依赖升级依赖)
  - [防火墙命令](#防火墙命令)

--------

## 配置网卡

- 修改网卡配置文件
  
  ```shell
  cd /etc/sysconfig/network-scripts  进入目录
  
  vi ifcfg-对应网卡名 修改网卡文件
  
  内容：
  
  设置ip
  
  IPADDR=""
  
  NETMASK="255.255.255.0"    设置子网掩码
  
  GATEWAY=""     设置网关
  
  BOOTPROTO="static" 静态IP
  
  ONBOOT="yes" 开机自启动
  
  NM_CONTROLLED="no" 取消NetworkManager权限
  ```

- 修改NetworkManager的配置文件

  > 位置： cd /etc/NetworkManager
  >
  > 文件：vi NetworkManager.conf
  >
  > 插入内容：dns=no

- 修改resolv.conf，配置dns

  > 位置：vi /etc/resolv.conf
  >
  > 主dns：nameserver 114.114.114.114

- 重启网关

  >systemctl restart network.service
  >
  >service network restart

--------

## 配置yum源、安装依赖、升级依赖

```shell
# 安装wget

yum install -y wget

# 进入yum源文件夹，备份yum源源文件

cd /etc/yum.repos.d/
mv CentOS-Base.repo CentOS-Base.repo.bk

# 下载163网易的yum源：

wget http://mirrors.163.com/.help/CentOS6-Base-163.repo

# 更新玩yum源后，执行下边命令更新yum配置，使操作立即生效
yum makecache

# 安装依赖
yum -y install gcc wget curl zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel libffi-devel 

# 升级依赖
yum upgrade

```

--------

## 防火墙命令

> 1、查看已开放的端口
> firewall-cmd --list-ports
>
> 2、开放端口（开放后需要要重启防火墙才生效）
> firewall-cmd --zone=public --add-port=3338/tcp --permanent
>
> 3、重启防火墙
> firewall-cmd --reload
>
> 4、查看防火墙状态
>
> systemctl status firewalld
>
> 5、关闭端口（关闭后需要要重启防火墙才生效）
> firewall-cmd --zone=public --remove-port=3338/tcp --permanent
>
> 6、开机启动防火墙
> systemctl enable firewalld
>
> 7、开启防火墙
>
> systemctl start firewalld
>
> 8、禁止防火墙开机启动
> systemctl disable firewalld
>
> 9、停止防火墙
> systemctl stop firewalld

## 常用工具

```sh
yum install -y zsh wget locate netstat dig iostat finger lsof
```

