# Maven

## 安装

###  windows安装

###  linux安装

+ yum安装

  ```sh
  yum install maven
  ```

  

+ 源码安装

  ```shell
  # 1. 下载
  wget -P /usr/local/ https://dlcdn.apache.org/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz 
  # 2. 解压
  cd /usr/local/; tar -zxvf apache-maven-3.8.4-bin.tar.gz
  # 3. 配置软连接（快捷方式）
  ln -s /usr/local/apache-maven-3.8.4/bin/mvn /usr/bin/mvn
  ```
  
  

### macOs安装

+ 进入官网 [官网](http://maven.apache.org/download.cgi)

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





