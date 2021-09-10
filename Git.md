# git
---

### 安装

#### 操作系统centos

```shell
# yum安装git
yum install -y git
# 查看git版本
git version
# OS Windows
# 在git官网下载安装程序，一直下一步。但是注意：过程中间git的默认主分支设置为main，而不是master
# OS macOS
```
#### windows

```shell
# 在git官网下载安装程序，一直下一步。但是注意：过程中间git的默认主分支设置为main，而不是master
# windows完成后如果想在cmd中用git，那么需要配置环境变量。如果不需要，那么用git bash或者xShell
# windows之后需要使用git，需要查看一下.ssh文件夹中的config文件，清空然后再测试git，
  git -T git@github.com，显示success就行
```



#### macOs

```shell
# Mac用Homebrew下载Git， 
# Mac安装完成不需要怎么去配置git
brew install git
```



### 配置

```shell
# 本机关联github仓库
ssh-keygen -t rsa -C "" # 先生成密钥对，引号内为自定义
cat /root/.ssh/id_rsa.pub # 查看公钥并传到github
git config --global init.defaultBranch main # 设置全局git默认分支main
git config --global user.name 'willgnicks' # 设置全局git用户名
git config --global user.email 'gnicksfaith@gmail.com' # 设置全局git邮箱
git config --global user.password '' # 设置全局git密码

```

### 常用命令

```shell
1	git clone    # 直接从仓库克隆项目
2	git init     # 如果仓库没有项目，想要将本地项目上传仓库
3	git remote add origin git@github.com:github账户:仓库名.git  #关联本地仓库与github仓库
4	git add .  # 将工作区项目添加暂存区
5	git commit -m '备注' # 将项目提交至本地仓库
6	git push -u origin main	# 将项目推送github
7	git pull	# 将项目从github下载
```


