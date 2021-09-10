# Django + uWSGI + Nginx

## (前提) 已搭建python环境并创建好venv虚拟环境，参考python搭建

## 一、上传代码

### 1. 使用scp将文件上传至服务器

```shell
scp -r 文件夹本地绝对路径 需上传的绝对路径
```



### 2. 使用git下载代码，具体方法参照git使用方法

## 二、创建uwsgi.ini配置文件

```python
[uwsgi]
socket=127.0.0.1:8000  # 提供给nginx的端口
# http=0.0.0.0:8000 即不使用nginx这样配置
# django项目根目录的绝对路径
chdir=/opt/Warehouse_Management_System
# django项目的wsgi协议入口
module=Warehouse_Management_System.wsgi:application

processes=2  # 处理进程数
threads=2    # 线程数
max-requests=5000  # 最大请求量 避免内存溢出
buffer-size=65536  # 缓存大小
master=True	# 是否为主线程
vacuum=True  # 服务器退出清除环境，删除socket和pid文件

home=/data/leatest # venv环境绝对路径
pidfile=/opt/project.pid # 服务进程文件路径
daemonize=/opt/project.log # django日志路径
```

## 三、配置django setting.py

```python
# 配置静态文件路径
STATIC_ROOT = '/data/leatest/static/'
STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static'), ]
# 在ROOT路径下创建静态文件夹
mkdir /data/leatest/static/
# 进入django根目录，收集静态文件
python3 manage.py collectstatic
```



## 四、安装nginx

```shell
#	 yum安装
yum -y install nginx
#  源码安装
tar -zvxf nginx-1.12.0.tar.gz  #解压源码
# 默认安装目录
/usr/local/nginx
./configure
make && make all
# 将nginx.conf、mime.types、uwsgi_params各复制一份至项目代码同级的scripts或conf目录中
vi scripts/nginx.conf
# 配置http中的server
# 动态数据由api接口返回
location / {
            include     /opt/Warehouse_Management_System/scripts/uwsgi_params;
            uwsgi_pass  127.0.0.1:8000;
        }
# 静态文件由nginx返回
location /static {
           alias  /opt/Warehouse_Management_System_static;
        }
#  测试nginx
/usr/local/nginx/sbin/nginx -t

```



## 五、进入venv环境

```shell
#  激活虚拟环境
source venv目录/bin/activate
#  启动uwsgi
uwsgi --ini /opt/project/uwsgi.ini   # 绝对路径
#  查看uwsgi是否启动
ps -aux |grep uwsgi
#	 重启uwsgi
uwsgi --reload /scripts/uwsgi.ini
#  停止uwsgi
uwsgi --stop /scripts/uwsgi.ini

```



## 六、开启nginx

```shell
# 使用scripts中的nginx.conf启动nginx
/usr/local/nginx/sbin/nginx -c /opt/project/scripts/nginx.conf
# 停止nginx
/usr/local/nginx/sbin/nginx -s stop
# 重启nginx
/usr/local/nginx/sbin/nginx -s restart
```

