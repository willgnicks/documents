# Python

- [Python](#python)
  - [Linux源码安装](#linux源码安装)
  - [pip使用](#pip使用)
    - [替换pip源在.pip文件夹下的pip.conf配置文件中](#替换pip源在pip文件夹下的pipconf配置文件中)
    - [一键安装环境（推荐在虚拟环境中操作）](#一键安装环境推荐在虚拟环境中操作)
    - [requirements.txt内容](#requirementstxt内容)
    - [virtualenv虚拟环境](#virtualenv虚拟环境)
    - [安装setuptools](#安装setuptools)
    - [问题](#问题)

---

## Linux源码安装

```shell

# 下载源码文件
wget http://npm.taobao.org/mirrors/python/3.9.2/Python-3.9.2.tar.xz

# 或者将Python-3.9.2.tar.xz上传至虚拟机
scp Python-3.9.2.tar.xz root@ip:/usr/local | cd /usr/local

# 解压python源码 # 进入源码目录
tar -xvf Python-3.9.2.tar.xz | cd Python-3.9.2

# 安装python到指定目录，prefix相当于将软件安装到该募路下
./configure --enable-optimizations --prefix=/usr/local/python3 --with-ssl 

# 编译
make && make install

# 设置软链接
ln -s /usr/local/python3/bin/python3  /usr/bin/python3
ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3

```

---

## pip使用

### 替换pip源在.pip文件夹下的pip.conf配置文件中

```shell
# 创建文件夹
mkdir /usr/local/.pip | cd /usr/local/.pip
# 创建配置文件 并 pip配置文件粘贴国内源
echo '[global]\nindex-url = https://pypi.tuna.tsinghua.edu.cn/simple\n[install]\nuse-mirrors = true\nmirrors = https://pypi.tuna.tsinghua.edu.cn/simple\ntrusted-host = https://pypi.tuna.tsinghua.edu.cn/simple' >> pip.conf
```

### 一键安装环境（推荐在虚拟环境中操作）

```shell
# 一键安装库
pip3 install -r requirements.txt
# 一键导出库，导出文件位置位于当前pwd路径下
pip3 freeze > requirements.txt
```

### requirements.txt内容

```properties
# requirement.txt
asgiref==3.3.4
backcall==0.2.0
colorama==0.4.4
decorator==5.0.9
Django==3.1.7
ipython==7.23.1
ipython-genutils==0.2.0
jedi==0.18.0
matplotlib-inline==0.1.2
numpy==1.20.3
parso==0.8.2
pickleshare==0.7.5
pip==20.2.1
prompt-toolkit==3.0.18
Pygments==2.9.0
PyMySQL==1.0.2
pytz==2021.1
setuptools==49.2.1
sqlparse==0.4.1
traitlets==5.0.5
wcwidth==0.2.5

```

---

### virtualenv虚拟环境

```shell
# 1. 安装virtualenv
pip3 install virtualenv

# 2. 设置软链接
ln -s /usr/local/python3/bin/virtualenv /usr/bin/virtualenv

# 3. 创建虚拟环境
virtualenv [环境名]
python3 -m virtualenv [环境名]

# 4. 激活虚拟环境
source 环境名/bin/activate

# 5. 退出虚拟环境
deactivate

echo '#java environment\nexport JAVA_HOME=/usr/local/jdk1.8.0_301\nexport CLASSPATH=.:${JAVA_HOME}/jre/lib/rt.jar:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar\nexport PATH=$PATH:${JAVA_HOME}/bin\n# maven enviro\nexport MAVEN_HOME=/usr/local/maven3.6\nexport PATH=$MAVEN_HOME/bin:$PATH' >> ~/.bash_profile

```

### virtualenv_wrapper虚拟环境管理

```less
# 1. 安装virtualenv_wrapper
pip3 install virtualenvwrapper
# 2. 配置worken_home
echo 'export WORKON_HOME=/usr/local/.virtualenvs\nexport VIRTUALENVWRAPPER_PYTHON=/usr/local/python3/bin/python3\nexport VIRTUALENVWRAPPER_VIRTUALENV=/usr/local/python3/bin/virtualenv\nsource /usr/local/python3/bin/virtualenvwrapper.sh' >> ~/.bash_profile
# 3. 查看环境中虚拟环境
workon
# 4. 新建虚拟环境
mkvirtualenv [虚拟环境名]
mkvirtualenv --python=[/other/python/you/installed] [虚拟环境名] # 指定python解释器
# 5. 运行切换虚拟环境
workon [虚拟环境名]
# 6. 退出虚拟环境
deactivate
# 7. 删除虚拟环境
rmvirtualenv [虚拟环境名]

```



### 配置说明

| 参数                                                         | 说明                           |
| ------------------------------------------------------------ | ------------------------------ |
| export WORKON_HOME=/usr/local/.virtualenvs                   | 配置虚拟环境的生成路径         |
| export VIRTUALENVWRAPPER_PYTHON=/usr/local/python3/bin/python3 | 配置环境中默认的python解释器   |
| VIRTUALENVWRAPPER_VIRTUALENV=/usr/local/python3/bin/virtualenv | 配置环境中默认的virtualenv路径 |
| source /usr/local/python3/bin/virtualenvwrapper.sh           | 配置环境的执行脚本             |

- 如果需要在bash中使用，修改~/.bashrc文件
- 如果需要在zsh中使用，修改~/.zshrc文件





---

### 安装setuptools

```shell
# 安装setuptool
wget --no-check-certificate  https://pypi.python.org/packages/source/s/setuptools/setuptools-19.6.tar.gz#md5=c607dd118eae682c44ed146367a17e26
# 解压
tar -zvxf setuptools-19.6.tar.gz
cd setuptools-19.6
# 安装
python3 setip.py

```

### 问题

```shell
# pip3升级后产生的问题
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py --force-reinstall

# 卸载python3
rpm -qa|grep python3|xargs rpm -ev --allmatches --nodeps

# 删除所有残余文件 成功卸载！   
whereis python3 |xargs rm -frv  

# 查看现有安装的python3        
whereis python3    
   
```
