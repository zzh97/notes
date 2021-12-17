#### 安装与运行

安装

```
pip3 install mitmproxy
```

![](./images/1.png)

查看版本

```
mitmproxy --version
```

![](./images/2.png)

运行，方法一（会出现一个终端）

```
mitmproxy
```

![](./images/3.png)

方法二（会出现一个网页）

```
mitmweb
```

![](./images/4.png)

方法三（会出现一个后台程序）

```
mitmdump
```

![](./images/5.png)

#### API文档

官网文档（英文）：https://docs.mitmproxy.org/stable/

PyTorch版（中文）：https://ptorch.com/docs/10/mitmproxy_introduction

由于mitmproxy更新的太快了，所以官方文档比较简略（跟不上啊），所以推荐用有以下方法来阅读文档

```
python -m pydoc -p 55555
```

![](./images/6.png)

而后，在浏览器里输入地址

![](./images/7.png)

在里面找到mitmproxy

![](./images/8.png)

打开它，就可以慢慢研究API了

![](./images/9.png)

如想要保存下来，离线查看

```
python -m pydoc -w mitmproxy.net.http
```

![](./images/10.png)



#### 为何运行没效果

mitmproxy的工作原理，是一个拦截器（相当于一个中间人）

A向B发生请求，B向A返回响应，这一个过程，我们记作A->b->A

加入mitmproxy后，就变成了，A->M->B->M->A



所以在之前的运行中，mitmproxy没有任何效果

因为我们没有把它设置成我们的中间人，我们仅仅是启动了它



如何设置呢？

以Chrome为例：地址栏输入 chrome://settings

![](./images/11.png)

![](./images/12.png)