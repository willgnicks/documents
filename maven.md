# Maven

## 1、安装

### 1.1 windows安装

### 1.2 linux安装

+ yum安装

  ```java
  yum install maven
  ```

  

+ 源码安装

  ```shell
  # 1. 进入想要安装的目录
  cd /usr/local/
  # 2. 下载
  wget https://dlcdn.apache.org/maven/maven-3/3.8.3/binaries/apache-maven-3.8.3-bin.tar.gz
  # 3. 解压
  tar -zxvf apache-maven-3.8.3-bin.tar.gz
  # 4. 修改配置文件
  vim ~/.zshrc
  # 5. 配置
  export M2_HOME=/Users/itkey/mac/Runtime/apache-maven-3.6.3
  export PATH=$PATH:$M2_HOME/bin
  # 6.使其生效
  source .zshrc
  ```

  

### 1.3 macOs安装

+ 进入官网 http://maven.apache.org/download.cgi

+ 下载后解压到你想要的位置，可随意。这里我的位置是：
  **/Users/gnicks/documents/Runtime/apache-maven-3.6.3**

+ 配置环境变量

``` shell
# 修改配置文件
vim ~/.zshrc

# 配置
export M2_HOME=/Users/gnicks/Documents/study/maven/apache-maven-3.8.3
export PATH=$PATH:$M2_HOME/bin

# 使其生效
source ~/.zshrc

```



## 2、国内镜像源

```xml
<mirror>
   <id>alimaven</id>
   <name>aliyun maven</name>
   <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
   <mirrorOf>central</mirrorOf>        
</mirror>
```



## 3、命令

+ 查看

  ```shell
  mvn -v
  ```

+ 创建mvn项目

  ```shell
  mvn archetype:generate
  ```

+ 





