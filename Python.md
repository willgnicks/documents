# Python

---

**问题**

```shell
## pip3升级后产生的问题
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py --force-reinstall
##卸载python3
rpm -qa|grep python3|xargs rpm -ev --allmatches --nodeps       卸载pyhton3
whereis python3 |xargs rm -frv           删除所有残余文件 成功卸载！
whereis python3       查看现有安装的python3
```



---

依赖环境

```markdown
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

## 安装： 

```shell
### 操作系统centos 
# 下载源码文件
wget https://www.python.org/ftp/python/3.9.2/Python-3.9.2.tar.xz

# 或者将Python-3.9.2.tar.xz上传至虚拟机

## 安装依赖
yum install zlib-devel

# 解压
tar -xvf Python-3.9.2.tar.xz

# 进入源码目录

# 切换目录/opt下
cd /usr/local/Python-3.9.2/

# 配置
./configure --enable-optimizations --prefix=/usr/local/python3 --with-ssl 
# 编译
make && make install
# 设置软链接
ln -s /usr/local/python3/bin/python3  /usr/bin/python3

# 安装依赖
yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
# 安装setuptool
wget --no-check-certificate  https://pypi.python.org/packages/source/s/setuptools/setuptools-19.6.tar.gz#md5=c607dd118eae682c44ed146367a17e26

tar -zvxf setuptools-19.6.tar.gz
cd setuptools-19.6
ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3
# 安装virtulenv
pip3 install virtualenv
# 设置软链接
ln -s /usr/local/python3/bin/virtualenv /usr/bin/virtualenv
# 创建虚拟环境
virtualenv -p /usr/bin/python3 文件夹名

pip3 install -r requirements.txt
# 解压
tar -xf Python-3.9.2.tar.xz
# 进入目录安装
cd Python-3.9.2
./configure --with-ssl
make && make install
# 安装venv
pip3 install virtualenv
# 
virtualenv 项目名
source 项目名/bin/activate 进入虚拟环境
deactivate	退出虚拟环境


# 创建项目目录并进入
mkdir -p /data/warehouse && cd  /data/warehouse

```

