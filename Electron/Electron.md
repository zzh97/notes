### 1 Hello World

#### 1.1 安装Electron

首先要确保你安装好了node.js，因为Electron是基于node.js，从而使用html、css、JavaScript来构建桌面应用的框架

```
mkdir my-electron-app && cd my-electron-app
npm init -y
npm i --save-dev electron
```

Electron应用的文件结构是这个样子的

```
my-electron-app/
├── package. // 配置 
├── main.js // 主脚本
├── preload.js // 预处理
└── index.html // 要渲染的页面
```

然后main.js中写入

```
// 为了管理应用程序的生命周期事件以及创建和控制浏览器窗口
// 从 electron 包导入了 app 和 BrowserWindow 模块
const { app, BrowserWindow } = require('electron')
// 该包为操作文件路径提供了实用的功能
const path = require('path')

// 使用preload.js创建一个浏览器窗口，并把index.html加载进窗口
function createWindow () {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })

  win.loadFile('index.html')
}

// electron app第一次初始化的时候，创建窗口
app.whenReady().then(() => {
  createWindow()
 // 添加一个新的侦听器，只有当应用程序激活后没有可见窗口时，才能创建新的浏览器窗口
 // 例如，在首次启动应用程序后或重启运行中的应用程序
  app.on('activate', () => {
    if (BrowserWindow.getAllWindows().length === 0) {
      createWindow()
    }
  })
})

// 添加了一个新的侦听器，当应用程序不再有任何打开窗口时试图退出
// 由于操作系统的 窗口管理行为 ，此监听器在 macOS 上是禁止操作的
app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit()
  }
})

```

在index.html中写入（HTML就不解析了）

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Hello World!</title>
    <meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline';" />
</head>
<body style="background: white;">
    <h1>Hello World!</h1>
    <p>
        We are using Node.js <span id="node-version"></span>,
        Chromium <span id="chrome-version"></span>,
        and Electron <span id="electron-version"></span>.
    </p>
</body>
</html>

```

在preload.js中写入

```
/* 预加载脚本就像是Node.js和您的网页之间的桥梁，
它允许你将特定的 API 和行为暴露到你的网页上，
而不是不安全地把整个 Node.js 的 API暴露*/

// 使用预加载脚本从process对象读取版本信息，并用该信息更新网页 

// 定义一个事件监听器，监听web页面被加载
window.addEventListener('DOMContentLoaded', () => {
  // 定义一个函数在index.html上使用预输出文本
  const replaceText = (selector, text) => {
    const element = document.getElementById(selector)
    if (element) element.innerText = text
  }
  // 遍历list，选择用于渲染的版本
  for (const type of ['chrome', 'node', 'electron']) {
    replaceText(`${type}-version`, process.versions[type])
  }
})

```

在package.json中写入

默认情况下， npm start 命令将用 Node.js 来运行主脚本
`"start": "electron ."`手动改为用electron

```
{
    "name": "my-electron-app",
    "version": "0.1.0",
    "author": "your name",
    "description": "My Electron app",
    "main": "main.js",
    "scripts": {
        "start": "electron ."
    }
}
```

> 注意：如果未设置 `main` 字段，Electron 将尝试加载包含在 `package.json` 文件目录中的 `index.js` 文件。

> 注意：`author` 和 `description` 字段对于打包来说是必要的，否则运行 `npm run make` 命令时会报错。

最后，运行程序

```
npm start
```

