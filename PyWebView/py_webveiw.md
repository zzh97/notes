#### 安装anacanda
anacanda是一个开源的python发行版本，集成了一下常用工具，如：jupyter notebook、NumPy等，相当于一个python全家桶

我们可以去它的官网上，下载最新版本
https://www.anaconda.com/products/individual

![](./py_img/1.png)
![](./py_img/2.png)
![](./py_img/3.png)
![](./py_img/4.png)
![](./py_img/5.png)
![](./py_img/6.png)
![](./py_img/7.png)
![](./py_img/8.png)
![](./py_img/9.png)
![](./py_img/10.png)
![](./py_img/11.png)
![](./py_img/12.png)
![](./py_img/13.png)
![](./py_img/14.png)

#### 如何运行一个网页
我们可以通过内嵌webview的方式，在Windows、Mac OS、Android、IOS等平台上，显示html文件，你可以当作是制作了一个简易的浏览器。

通过pip（python的包管理工具，装python时会自带，无需特定安装）安装pywebview
（如果pip行不通，可以试试pip3）
```
pip install pywebview
```
![](./py_img/15.png)
![](./py_img/16.png)
![](./py_img/17.png)
![](./py_img/18.png)
然后再运行`pip install pywebview`
![](./py_img/19.png)
https://slproweb.com/products/Win32OpenSSL.html
去这里下载一个东西就好了
![](./py_img/20-1.png)
再运行`pip install pywebview`
![](./py_img/20.png)
现在，就成功安装pywebview了

此时，新建一个python文件，然后编写代码
```
import webview

webview.create_window('Title', html='<h1>hello world</h1>')
webview.start()
```
![](./py_img/21-1.png)
编写好后，在(同级目录下的)终端运行它
```
python a.py
```
此时，你有可能需要将python也添加至环境变量
![](./py_img/21.png)
![](./py_img/22.png)
然后运行`python a.py`就好了
![](./py_img/23.png)

#### 如何打包成.exe文件
```
pip install auto-py-to-exe
```
![](./py_img/24.png)
```
auto-py-to-exe
```
![](./py_img/25.png)
如果，在a.py中，写的并不是
```
webview.create_window('Title', html='<h1>hello world</h1>')
```
而是，引的一个外部html文件
```
webview.create_window('Title', 'index.html')
```
这时一定要选“单目录”，打包成功后，把index.html放入导出的文件夹里就好了
