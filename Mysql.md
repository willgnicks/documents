# Mysql

- [Mysql](#mysql)
  - [安装](#安装)
    - [Centos 8 DNF安装](#centos-8-dnf安装)
    - [centos 7 Yum安装](#centos-7-yum安装)
  - [关闭防火墙对应端口](#关闭防火墙对应端口)
  - [查看RSA加密](#查看rsa加密)
  - [Mysql_8.0 设置明文密码](#mysql_80-设置明文密码)
    - [密文密码自动设置机制](#密文密码自动设置机制)
    - [重置密码（忘记原明文密码）](#重置密码忘记原明文密码)
  - [配置](#配置)
    - [配置文件（/etc/mysql/my.conf）](#配置文件etcmysqlmyconf)
    - [相关命令及远程访问](#相关命令及远程访问)
  
---

## 安装

### Centos 8 DNF安装

```shell
# 安装mysql
1  dnf install @mysql 
# 开机自启动
2  sudo systemctl enable --now mysqld
3  sudo systemctl status mysqld
# 执行安全性等脚本
4  sudo mysql_secure_installation 
     # 选择密码验证策略等级， 我这里选择0 （low），回车
     # 输入新密码两次
     # 确认是否继续使用提供的密码？输入y ，回车
     # 移除匿名用户？ 输入y ，回车
     # 不允许root远程登陆？ 我这里需要远程登陆，所以输入n ，回车
     # 移除test数据库？ 输入y ，回车
     # 重新载入权限表？ 输入y ，回车
5  use mysql;
6  update user set host='%' where user='root';
7  flush privileges;

```

### centos 7 Yum安装

```shell
# 下载rpm
1  wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm 
2  rpm -ivh mysql80-community-release-el7-3.noarch.rpm
3  yum -y install mysql-server
4  systemctl start mysqld
# 拿临时密码 -JLc9KRgi?#h
5  grep "A temporary password is generated for root@localhost" /var/log/mysqld.log  
# 输入临时密码
6  mysql -uroot -p  
 #设置密码
7  set password='@Wbw31415926'
# 设置远程连接
8  use mysql  
9  update user set user.Host='%' where user.User='root';
10  flush privileges;

# 不设置若口令至此结束
   
# 查看口令强度
show variables like 'validate_password%';
validate_password.check_user_name  检查是否密码为用户名
validate_password.dictionary_file   指定密码验证的文件路径；
validate_password.length   固定密码的总长度；
validate_password.mixed_case_count 整个密码中至少要包含大/小写字母的总个数；
validate_password.number_count   整个密码中至少要包含阿拉伯数字的个数；    
validate_password.policy       指定密码的强度验证等级，默认为 MEDIUM；
validate_password.special_char_count 特殊字符设置
# 设置弱口令
set global validate_password.policy=LOW;
set global validate_password.length=3;
set global validate_password.mixed_case_count=0;
set global validate_password.number_count=0;
set global validate_password.special_char_count=0;
set global validate_password.check_user_name=OFF;
# 设置弱口令
set password='root';

```

---

## 关闭防火墙对应端口

```shell
# 查看防火墙某个端口是否开放
  ​firewall-cmd --query-port=3306/tcp
# 开放防火墙端口3306
  firewall-cmd --zone=public --add-port=3306/tcp --permanent
# 查看防火墙状态
  systemctl status firewalld
# 关闭防火墙
  systemctl stop firewalld
# 打开防火墙
  systemctl start firewalld
# 开放一段端口
  firewall-cmd --zone=public --add-port=40000-45000/tcp --permanent

以上命令执行完成后，请使用firewall-cmd --reload重新加载防火墙配置或者使用systemctl restart firewalld重启防火墙，以使防火墙新的配置生效。
```

---

## 查看RSA加密

```shell
# 进入存放密钥的目录，查看公私密钥，可自定义配置
cd /var/lib/mysql   
    
# 获取公钥
1 SHOW STATUS LIKE 'Rsa_public_key'\G; 
    cat public_key.pem  # 获取公钥
    -----BEGIN PUBLIC KEY-----
    MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA1vQ1rUzwCcXDf1aw8iX8
    tfqZNIe9/uVnA1lWc5M3aWpNY4qx+De1ssstN8ZABaBM7PfbglNLlugHjWqoXLdQ
    mov4tS/T/ZprPfgBCh8o4A1siSzkVlLoehjnE9czoUkipWhVzsASlwQ+HfML8Yac
    CuJMPbhC8Uhfh05Phi2pUF35//32gSWDc84EU6Giw/Xt0WApLBdDNf4UxqOvpOMw
    FeTanAYJph3aBCHg0QZoZ3ViScvvJ5An/e0fg7PEdEJg8D4L5qjmANUBjB8Zw0Ev
    9Dj0tj/cbcmo9VERIgQiMwk4MNHOPLvrRdeRzI1FV4wLnuOTBoyTRazs5qFHOwcM
    JwIDAQAB
    -----END PUBLIC KEY-----
# 查看私钥
2 SHOW STATUS LIKE 'Rsa_public_key'\G;
    cat private_key.pem        
    -----BEGIN RSA PRIVATE KEY-----
    MIIEpQIBAAKCAQEA1vQ1rUzwCcXDf1aw8iX8tfqZNIe9/uVnA1lWc5M3aWpNY4qx
    +De1ssstN8ZABaBM7PfbglNLlugHjWqoXLdQmov4tS/T/ZprPfgBCh8o4A1siSzk
    VlLoehjnE9czoUkipWhVzsASlwQ+HfML8YacCuJMPbhC8Uhfh05Phi2pUF35//32
    gSWDc84EU6Giw/Xt0WApLBdDNf4UxqOvpOMwFeTanAYJph3aBCHg0QZoZ3ViScvv
    J5An/e0fg7PEdEJg8D4L5qjmANUBjB8Zw0Ev9Dj0tj/cbcmo9VERIgQiMwk4MNHO
    PLvrRdeRzI1FV4wLnuOTBoyTRazs5qFHOwcMJwIDAQABAoIBAQCsRCbIbkJo8o8M
    fENurLbseJtTl/3SS7LU4kIAedkMqF7BCaQ7UxpQ4bepXT5tw9wihTjsJykLFYUH
    9pRbSaZVVRvKyTvRoHGVxi2/GN2/QcLb5JhR/jvFrjNymSMNfPlBKm6qNRAw6vuF
    MQU/WSuxJU8In6U2jVPRshbVZ76rYk026TwKln7KFVIvmGxQGx4roxDunuh/nwVk
    npU/GFFAbt2nzwrmfxMyhlwN8716F/vAvz37vzB4zIR69HEESabBjZJAcD8pOAmu
    SbaUPjLe+CGiZec0Bp48bXw2kZZmGo1Y3Jjwc7H40TCnhZ+aPRqOhZzAmzohe8I9
    NVpFzH1BAoGBAOzlqDD0okaK//0CuOPsYC4bhogXOzQZiv1jLw43sJKFAr4h0VZ8
    xRRmrO2E5OBQmlwmr3du30ZWp9IRRTLt2rk/9gKBRd+04lk52yb/o7Vvo7IRHyrF
    sVVVolOkYS8nd28i9sbI8MxPPpQ9CuuEjo3jSQ5A0bXtJEMphZtjx7nXAoGBAOhJ
    kragBq/eRC+1YcLilXR/okGRt3BghjZrSJkh3/BB0HJnwjjfExoz9oMcy1SIBrJ0
    R8kYbFmRNxpPXOAcuuj/DkdspZkAWo9psYtOQGp57FvBChHzXMwjCFBtM615Hb6M
    XoZcOo05R7E33GPxjrKofIHWStpl/K3KDkoUTBYxAoGBAKFdOfjG2jaU/hP4o7pV
    S5p8k2Hl+STe9UbuJaJYmsTjJ2Adpvtzl8byvX441LJbFRoKG+GNuzatVjkIHIu5
    axBemhNQvSjJjJjciQQChB/VgLqNYR6AdO+8mgrBYJV/G6KvPUtgmm2A2Q6eme6d
    Z4EMvbmgu3hhpR6+jMyw5d4XAoGAHiJdTB/afjpBckb/lb67UM+2BveWape7EZg9
    ZNBGMu720cCwK5yU59NR6ZR0tFSpOcFoBqiKddwm39zn2ZMglFVyTsXDfePT28ME
    a2QNa0LB7O1QFyARK9Jno7dm+tw5hZzELn4MgoGp0U3D45tUvcypylY4g7izXQBX
    djjH3iECgYEAlIIgRIgfZfmGLrdFl7lCu8xJmoYBFjbwIkqh8aRTajzPQtippX+L
    81Le7PyjDcsQpvtVMfFBCO+PmhuIQ+UEVpdqREl3V5hapIpTecIlVdr3KWdMuFuB
    nLlrD0VUhLjt9Oly/8ObvoKGHhEN1Gtephjr7YDFyLz1WLZHPTHmiTY=
    -----END RSA PRIVATE KEY-----
```

---

## Mysql_8.0 设置明文密码

### 密文密码自动设置机制

```shell
# mysql8用户设置的密码会被加密存储在mysql数据库的user表中的authentication_string字段下

1 mysql -u[用户名] -p[原密码]   # 先进入mysql
2 set password='新密码'  # 数据库会自动根据SHA-256算法加密新密码原文成密文，存在当前用户的authentication_string字段下
```

### 重置密码（忘记原明文密码）

```shell
# 注意事项
# 不要直接修改用户的authentication_string成想要的明文密码
# 由于自动加密的和解密的机制，如果直接设置密文密码，那么你想要输入的明文密码一定和数据库中存放的密文密码不是一样的
# 例如：需要将密码改成root，直接修改authentication_string为root，那么在加密过程root的加密密文一定不等于数据库中的root
# 此外，根据公钥和私钥可以算出N多中的密文，我们直接通过密钥算法算出加密后的密文直接存在authentication_string也是不行的
# 因为自动加密的过程中还加有其他盐分
# 不要在跳过表验证后直接设置明文密码，此时因为是跳过验证登录，数据库有写禁用
# 不要在此时 set password='新密码'

# 所以重置密码需要绕过表验证，然后在绕过加密机制

# 首先找到mysql配置文件
vi my.conf  
# 表中加入该值跳过表验证
skip-grant-tables  
# 重启mysql
service mysqld restart 
# 跳过表验证直接以root身份登录
mysql 
# 可查看当前登录用户
select user();
# 进入数据库
use mysql
# 先将密文设置为空，那么此时为空的密文是不需要有原文的，按照加密规则，任何有效数据都会被加密
update user set authentication_string='' where user='root';  
# 刷新
flush privileges; 
# 退出   
exit 
# 进入配置文件注释掉该值 skip-grant-tables 
vi my.conf
# 重启mysql
service mysqld restart 
# 无密码登录
mysql -uroot
# 设置新密码
set password='新密码';  
# 刷新
flush privileges;

# 此时绕过加密机制，重新设置了明文密码，且该明文密码被加密存入数据库，如果是强口令，几乎不会被强破

/etc/mysql/my.conf配置
```

---

## 配置

### 配置文件（/etc/mysql/my.conf）

```shell
# 关闭msyql反向dns解析  
  skip-name-resolve  
# 跳过表验证
  skip-grant-tables  
```

### 相关命令及远程访问

```shell
# 查询版本
  mysqladmin --version  
# 开启服务
  service mysql start  
# 重启
  sevice mysql restart 
# 查状态
  service mysql stauts 
# 登录
  mysql -uroot -proot  
# 授权用户
  GRANT ALL ON . TO '用户名'@'%';
# 创建用户    
  create user gnicks identified by 'root';
# 刷新    
  flush privileges;
# 授权
  alter user '用户名'@'登录主机' identified by '密码(自定义)';
```
