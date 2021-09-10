# SSH

## SSH信任

----

### 1. 手动添加Authorized_keys

```shell
# 访问设备  生成密钥对
ssh-keygen -t rsa -C '自定义内容'
# 查看公钥并复制
cat ~/.ssh/irsa.pub         
# 被访问设备粘贴公钥
vi ~/.ssh/authorized_keys          
# 则被放访问设备信任该访问设备
ssh root@ip      # 即可直接进入该被访问设备
```



----

### 2. 自动上传id_rsa.pub

```shell
# 访问设备  生成密钥对
ssh-keygen -t rsa -C '自定义内容'
# 上传公钥
ssh-copy-id root@ip
```



## 内网穿透

----

#### 公网服务器设置

```shell
# 登录公网服务器，修改ssh配置
vi /etc/ssh/sshd_config
# 设置以下几项
GatewayPorts yes
TCPKeepAlive yes
ClientAliveInterval 60
ClientAliveCountMax 3
# 保存并重启ssh
service sshd restart
# 开放安全组中的需要映射的端口，例
TCP 8080		# 入站出站均暴露该端口
```



----

#### 内网转发机或源机设置

```shell
# 安装autossh，安装之前最好update包源
# centos用yum
yum -y install autossh
# ubuntu用apt
apt -y install autossh
# 源机在公网服务器上ssh信任
# 访问设备  生成密钥对
ssh-keygen -t rsa -C '自定义内容'
# 上传公钥
ssh-copy-id root@ip
# 建立通道
autossh -M 65532 -NR 8888:127.0.0.1:8080 root@targetIP -f
# 60003是内网服务器端口，用来监听内网服务端口
# 8888是外网安全组添加的开放端口，监听请求
# 8080是内网服务器对外提供服务的端口
# -f 选项时后台运行
autossh -M 60003 -NR 60002:127.0.0.1:8080 root@huashengshu.top -f
```

