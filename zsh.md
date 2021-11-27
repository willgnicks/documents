# Linux安装ZSH

## 1. 安装zsh

```sh
# 以实际系统为准，ubuntu使用apt
echo $SHELL

cat /etc/shells

yum install -y zsh
```



## 2. 设置zsh为默认shell

```sh
chsh -s /bin/zsh
```



## 3. 安装oh_my_zsh(使用git)

```shell
# 下载oh_my_zsh
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
# 复制启动sh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```



## 4. 配置主题

```shell
# 下载zsh高亮插件
git clone https://github.com/zsh-users/zsh-syntax-highlighting ~/.zsh/zsh-syntax-highlighting

# 下载德古拉主题
git clone https://github.com/dracula/zsh.git ~/.zsh/zsh-master
wget https://github.com/dracula/zsh/archive/refs/heads/master.zip ~/.zsh/
unzip master.zip

# 追加配置文件
echo 'source ~/.zsh/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh' >> ~/.zshrc
# 创建快捷方式/软连接
ln -s ~/.zsh/zsh-master/dracula.zsh-theme ~/.oh-my-zsh/themes/dracula.zsh-theme
# 设置随机主题
sed -i '/^ZSH_THEME.*/cZSH_THEME="random"' ~/.zshrc
# 生效配置文件
source ~/.zshrc
# macOS可以下载iterm的dracula配色，在iterm中选择配色
git clone https://github.com/dracula/iterm.git
```



## 5. 注意配置文件

```sh
# 配置文件 .zshrc 中配置omz的路径
export ZSH="/root/.oh-my-zsh" # omz的安装路径
source $ZSH/oh-my-zsh.sh # 指定sh脚本路径
```

