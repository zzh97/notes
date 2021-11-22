#### linux命令
```
pwd // 查看当前路径
ls // 查看该路径下的文件
ls -a // 全部文件（包括隐藏文件）
ls -alh // 最常用
```

#### 科学上网
1.先去vultr上租一台vps（我是用的5$/mo），选择linux系统（我用的是Ubuntu16.04），地址我选的东京（首尔也不错）
具体见：https://www.vultrcn.com/1.html
2.然后在终端上安装ssr服务器
```
wget -N --no-check-certificate https://raw.githubusercontent.com/luvvien/ssr-install-shellscript/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```
如果不行，则需先安装wget
```
apt-get install -y wget
```
3.开始配置ssr服务器
具体见：https://viencoding.com/article/155
4.在电脑或手机上安装ssr客户端
5.然后配置，就OK了
关于ssr客户端的配置，极其简单，你一看就懂（实在不行就用二维码是形式），故不做赘述

如果你还想用这个vps做网站什么的，可以取给它配置一个域名，取阿里云/腾讯云买一个域名（推荐.cc不用认证），然后解析一下就好了

具体的解析方法，阿里云/腾讯云上有教

#### 扩展问题

DNS域名污染
域名劫持
数字签名
SSH
SQL注入
DDos攻击
CSRF(设置id给用户) Xss(关闭js获取cookie)
反向代理