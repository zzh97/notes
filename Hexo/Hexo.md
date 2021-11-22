#如何快速搭建个人博客
##一、准备工具
###1.github账号
###2.Git工具（Git需要github）
###3.Node.js
###4.Hexo框架（Hexo需要Node和Git）
##二、开始搭建
###1.注册github账号（去官网注册就好了，过程略）
###2.下载Git工具（去官网下就好了，过程略）
###3.下载Node.js（去官网下就好了，过程略）
###4.设置cnpm（因为npm太慢了）
```
	npm install -g cnpm --registry=https://registry.npm.taobao.org
```
###5.安装Hexo
```
	cnpm install -g hexo-cli
```
###6.创建一个文件夹（放你的博客，过程略）
###7.搭建Hexo（注意要先将Git设为环境变量）
```
	hexo init
```
注：在此过程中，如果安装错误，直接把这个文件夹删除，再新建一个来安装就好了
```
	//要是一直报错，可以试试初始化Git
	git init
```
###8.启动Hexo
```
	hexo s
```
成功的话，就可以通过localhost:4000来访问
###9.更换Hexo主题（以Next为例）
```
	git clone https://github.com/iissnan/hexo-theme-next themes/next
```
在blog文件夹下，找到_contig.yml  
打开修改theme: landscape为theme: next
```
	//很多时候，如果要更新，就做以下两步
	hexo clean //清理文章
	hexo g //生成文章
```
###14.Next主题配置
####①设置中文（在blog/_contig.yml中）
```
	//搜索Site，改为zh-Hans或者zh-CN
	//看你language文件下有哪个，就改为哪个
	//顺便把作者、标题也改了
	# Site
	title: 自闭者の自习室
	subtitle:
	description:
	keywords:
	author: 张子涵
	language: zh-Hans
	timezone:
```
####②设置标签和分类（在next/_contig.yml中）
```
	//搜索menu，想打开哪个，就把那个的#去掉
	home: / || home
	#about: /about/ || user
	#tags: /tags/ || tags
	#categories: /categories/ || th
	archives: /archives/ || archive
	#schedule: /schedule/ || calendar
	#sitemap: /sitemap.xml || sitemap
	#commonweal: /404/ || heartbeat
```
####③设置头像和标签（在next/_contig.yml中）
```
	//搜索avatar，想打开哪个，就把那个的#去掉
	# Sidebar Avatar
	# in theme directory(source/images): /images/avatar.gif
	# in site  directory(source/uploads): /uploads/avatar.gif
	avatar: /images/avatar.gif
```
####④设置链接（在blog/_contig.yml中）
```
	//搜索URL	
	# URL
	## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
	url: http://zzh97.com
	root: /
	permalink: :year/:month/:day/:title/
	permalink_defaults:
```
####⑤侧边栏社交链接（在next/_contig.yml中）
```
	//搜索Social，想打开哪个，就把那个的#去掉
	#social:
	GitHub: https://github.com/zzh97 || github
	E-Mail: mailto:wzdzzh@outlook.com || envelope
	#Google: https://plus.google.com/yourname || google
	#Twitter: https://twitter.com/yourname || twitter
	#FB Page: https://www.facebook.com/yourname || facebook
	#VK Group: https://vk.com/yourname || vk
	#StackOverflow: https://stackoverflow.com/yourname || stack-overflow
	#YouTube: https://youtube.com/yourname || youtube
	#Instagram: https://instagram.com/yourname || instagram
	#Skype: skype:yourname?call|chat || skype
```
####⑥更改样式（在next/_contig.yml中）
```
	//搜索scheme，想打开哪个，就把那个的#去掉
	# Schemes
	#scheme: Muse
	scheme: Mist
	#scheme: Pisces
	#scheme: Gemini
```
###15.新建文章
```
	hexo n "title of article"
```
进到文章目录下打开文章，进行编辑（MarkDown语法）  
如: D:\blog\source\_posts\first-note.md
```
	hexo clean //清理页面
	hexo g //生成页面
```
###16.部署到github.io上（免费，但只能静态）
####①创建github仓库并安装hexoGit
在github上新建一个仓库，名叫“你的昵称.github.io”  
然后安装hexo-git
```
	cnpm install hexo-deployer-git --save
```
####②修改配置文件
修改Git(你刚开始新建的那个文件夹)中的_config.yml文件，在最底下改为：
```
	deploy:
	  type: git
	  repo: https://github.com/zzh97/zzh97.github.io.git
	  branch: master
```
repo中写你刚刚创建的仓库的地址

####③设置git的global身份（在Git bash中）
```
	$ git config --global user.name 'zzh97'
	$ git config --global user.email 'wzdzzh@163.com'
	//下面这句是生成SSH公钥的，然后把复制到github上
	//如果配置了SSH，后面的hexo d就不需要输入账号密码了	
	$ ssh-keygen -t rsa -C 'wzdzzh@163.com'
```
####④部署Hexo（在命令行中）
```
	hexo d
```
然后输入你的github账号和密码
	