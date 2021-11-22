#### 安装Qt

```
pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple
```

需要先给pip3配置环境变量（我用的是anaconda）

注意：如果用的是http的链接，可能会报`The repository located at pypi.tuna.tsinghua.edu.cn is not a trusted or secure host`这种错误

但是，如果用https的链接，也可能会报`pip is configured with locations that require TLS/SSL, however the ssl module in`这种错误

这时，我们需要把anaconda里的东西都添加进环境变量

```
D:\...\Anaconda3\condabin
D:\...\Anaconda3\Scripts
D:\...\Anaconda3\Library\bin
D:\...\Anaconda3\
```

如上

随后安装tools

```
pip3 install pyQt5-tools -i https://pypi.tuna.tsinghua.edu.cn/simple
```

然后，创建一个qt.py，写入

```
import sys
from PyQt5 import QtWidgets,QtCore
app = QtWidgets.QApplication(sys.argv)
widget = QtWidgets.QWidget()
widget.resize(360,360)
widget.setWindowTitle("Hello, Qt")
widget.show()
sys.exit(app.exec_())
```

再回到cmd中

```
python qt.py
```

如果能打开一个名为"Hello, Qt"的窗口，就说明安装成功了

不过我们一般会用图形化界面来设计窗口，即designer.exe

在anaconda中找到我们刚刚安装的qt（搜索designer.exe即可）

我的是在`D:\...\Anaconda3\Lib\site-packages\qt5_applications\Qt\bin`

双击designer.exe，就可以打开了



#### 设计浏览器

使用PyQtWebEngine，在应用程序中嵌入 Web 内容的能力，并且基于 Chrome 浏览器

这是它的官网：https://pypi.org/project/PyQtWebEngine/

```
pip3 install PyQtWebEngine -i https://pypi.tuna.tsinghua.edu.cn/simple
```

编写python代码，运行后，便可打开一个网页

```
from PyQt5.QtCore import *
from PyQt5.QtWidgets import *
from PyQt5.QtWebEngineWidgets import *
import sys

class MainWindow (QMainWindow):
    def __init__ (self):
        super (QMainWindow, self).__init__ ()
        self.setWindowTitle ('显示网页')
        self.resize (800, 800)
        # 新建一个QWebEngineView对象
        self.qwebengine = QWebEngineView (self)
        # 设置网页在窗口中显示的位置和大小
        self.qwebengine.setGeometry (20, 20, 600, 600)
        # 在QWebEngineView中加载网址
        self.qwebengine.load (QUrl (r"https://www.baidu.com/"))

if __name__ == '__main__':
    app = QApplication (sys.argv)
    win = MainWindow ()
    win.show ()
    sys.exit (app.exec_ ())
```

通过PyQt5提供的命令行工具，将design.exe中保持的.ui文件，转换为.py文件

```
pyuic5 -o untitled.py untitled.ui
```

使用design绘制的.ui文件

```
from PyQt5.Qt import *
from untitled import Ui_Form
from PyQt5.QtWebEngineWidgets import *
import sys

class MainWindow (Ui_Form, QMainWindow):
    def __init__ (self):
        super (MainWindow, self).__init__ ()
        self.setupUi (self)
        self.retranslateUi (self)
        self.wb = QWebEngineView ()
        self.wb.load (QUrl ('http://www.baidu.com'))
        self.setCentralWidget (self.wb)

if __name__ == '__main__':
    app = QApplication (sys.argv)
    ui = MainWindow ()
    ui.show ()
    sys.exit (app.exec_ ())
```

能够点击

```
from PyQt5.Qt import *
from untitled import Ui_Form
from PyQt5.QtWebEngineWidgets import *
import sys

# 改下刷新窗口的方法
class WebEngineView (QWebEngineView):
    def createWindow (self, QWebEnginePage_WebWindowType):
        return self

class MainWindow (Ui_Form, QMainWindow):
    def __init__ (self):
        super (MainWindow, self).__init__ ()
        self.setupUi (self)
        self.retranslateUi (self)
        self.wb = QWebEngineView ()
        self.wb.load (QUrl ('http://www.baidu.com'))
        self.setCentralWidget (self.wb)

if __name__ == '__main__':
    app = QApplication (sys.argv)
    ui = MainWindow ()
    ui.show ()
    sys.exit (app.exec_ ())
```

安装PyInstaller，用于打包.py文件

```
pip3 install pyinstaller -i https://pypi.tuna.tsinghua.edu.cn/simple
```

打包

```
pyinstaller -F -w main.py
```

