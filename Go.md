## 安装

```sh
# 下载
wget https://golang.google.cn/dl/go1.17.4.linux-amd64.tar.gz 
# 解压
tar -C /usr/local -xzf go1.17.4.linux-amd64.tar.gz
# 添加软连接
ln -s /usr/local/go/bin/go /usr/bin/go
```

## 插件

```sh
git clone https://github.com/Go-zh/tools.git $GOPATH/src/github.com/Go-zh/tools

  gopkgs
  go-outline
  gotests
  gomodifytags
  impl
  goplay
  dlv
  dlv-dap
  staticcheck
  gopls
  goimports
```

## 框架

```sh
# 设置代理
go env -w GOPROXY=https://mirrors.aliyun.com/goproxy
echo "export GO111MODULE=on" >> ~/.profile
$ echo "export GOPROXY=https://goproxy.cn" >> ~/.profile
$ source ~/.profile
https://mirrors.aliyun.com/goproxy
# 关闭代理
go env -w GO111MODULE=off
# 安装gin框架
go get -u github.com/gin-gonic/gin

```

