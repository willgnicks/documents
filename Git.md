# Git

---

## 安装

### 操作系统centos

```shell
# yum安装git
yum install -y git
# 查看git版本
git version
# OS Windows
# 在git官网下载安装程序，一直下一步。但是注意：过程中间git的默认主分支设置为main，而不是master
```

### windows

```shell
# 在git官网下载安装程序，一直下一步。但是注意：过程中间git的默认主分支设置为main，而不是master
# windows完成后如果想在cmd中用git，那么需要配置环境变量。如果不需要，那么用git bash或者xShell
# windows之后需要使用git，需要查看一下.ssh文件夹中的config文件，清空然后再测试git，
  git -T git@github.com，显示success就行
```

### macOs

```shell
# Mac用Homebrew下载Git， 
# Mac安装完成不需要怎么去配置git
brew install git
```

## 配置

```shell
# 本机关联github仓库

# 先生成密钥对，引号内为自定义
ssh-keygen -t rsa -C "" 
# 查看公钥并传到github
cat /root/.ssh/id_rsa.pub 
# 设置全局git默认分支main
git config --global init.defaultBranch main 
# 设置全局git用户名
git config --global user.name 'willgnicks' 
# 设置全局git邮箱
git config --global user.email 'gnicksfaith@gmail.com' 
# 设置全局git密码
git config --global user.password '' 

```

### 常用命令

```shell
# 直接从仓库克隆项目
git clone    
# 如果仓库没有项目，想要将本地项目上传仓库
git init     
#关联本地仓库与github仓库
git remote add origin git@github.com:github账户/仓库名.git  
# 将工作区项目添加暂存区
git add .  
# 提交
git commit -m '备注' 
# 推送
git push -u origin main
# 下载
git pull
# 回滚
git reset --[模式] [版本]
    # 模式
    --hard # 工作区和暂存区全部回滚
    --soft 
    --mixed # 只回滚暂存去
    # 版本
    HEAD^ # 前一个版本
    HEAD2 # 前两个版本
    HEAD3 # 前三个版本
    版本号 # 具体版本
# 关联库
git remote
    -v # 查看库
    add [远端库名] [远端库地址] # 添加库
    remove [远端库名] # 删除库
# 合入
git merge
# 分支
git branch
# 切换/回滚工作区
git checkout [分支/文件名]
# 查看状态
git status
# 查看文件变更
git diff
# 查看日志
git log

```
