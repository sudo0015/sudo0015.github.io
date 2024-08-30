## 说在前面的话

> 本人是一只爱搞开发的中学牲，Qt的学习还在路上，这篇博文是我在艰苦摸索后的经验总结，希望看到这篇文章的你能少走些弯路。
## 艰辛历程
上来就找了很多文章，一通Ctrl+C、Ctrl+V之后，发现竟没有一个能跑起来！其中相对来说对我最有启发的是这篇[python3 pyqt5 实现热键唤出窗口](https://blog.csdn.net/qq_43036532/article/details/105834639)，在这里有必要把代码贴上来。
> hotKet.py

```python
import win32con
from ctypes import *
from ctypes.wintypes import *
from mainwindow import QMThread
from PyQt5.QtCore import pyqtSignal

main_key = 192

# 这里的 QMThread 为自定义的 QThread
class HotKey(QMThread):
    """全局热键监听"""
    ShowWindow = pyqtSignal(int)

    def __init__(self):
        super(HotKey, self).__init__()

        self.main_key = 192

    def run(self):
        """ 监听 windows 快捷键使用 """

        user32 = windll.user32

        while True:
            if not user32.RegisterHotKey(None, 1, win32con.MOD_ALT, self.main_key):  # alt+~
                print('Unable to register id', self.key_num, self.key_num % 2)

            try:
                msg = MSG()

                if user32.GetMessageA(byref(msg), None, 0, 0) != 0:
                    print('2222222', msg.message, win32con.WM_HOTKEY)
                    if msg.message == win32con.WM_HOTKEY:
                        if msg.wParam == win32con.MOD_ALT:
                            self.ShowWindow.emit(msg.lParam)

            finally:
                print('finish')

```

> mainwindow.py

```python
import sys, os
from PyQt5.QtCore import *
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
import hotKey

class UUMainWindow(QWidget):
    """主窗口页面"""
    ShowWindow = pyqtSignal(int)

    def __init__(self, parent=None):
        super(UUMainWindow, self).__init__(parent)

        self.setWindowTitle('主页面')
        self.setGeometry(300, 100, 1300, 800)
      
    def hot_key_event(self, data):
        """热键处理函数"""
        if data == 12582913:
            if self.isMinimized():  # 判断窗口是否为最小化
                self.showNormal()   # 如果为最小化, 则恢复正常
            else:
                self.showMinimized()  # 将窗口设置为最小化


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = UUMainWindow()

    hot_key = hotKey.HotKey()
    hot_key.ShowWindow.connect(main.hot_key_event)

    hot_key.start()  # 开启热键监听的线程

    main.show()
    sys.exit(app.exec_())

```
这篇博文给我提供了一个思路：写一个hotKey.py，里面再开一个线程，再把信号绑定，不就可以了吗？但上面的代码有明显的问题：`from mainwindow import QMThread`是什么鬼？`QTread`吧。再把PyQt改成PySide（个人习惯），加一个Messagebox，代码如下：

> hotKey.py

```python
import win32con
from ctypes import *
from ctypes.wintypes import *
from PySide6.QtCore import *
from PySide6.QtGui import *
from PySide6.QtWidgets import *
import tkinter.messagebox
main_key = 192
class HotKey(QThread):
    ShowWindow = Signal(int)
    def __init__(self):
        super(HotKey, self).__init__()
        self.main_key = 192
    def run(self):
        user32 = windll.user32
        while True:
            if not user32.RegisterHotKey(None, 1, win32con.MOD_ALT, self.main_key):  # alt+~
                tkinter.messagebox.showerror("错误","全局热键注册失败。")
            try:
                msg = MSG()
                if user32.GetMessageA(byref(msg), None, 0, 0) != 0:
                    if msg.message == win32con.WM_HOTKEY:
                        if msg.wParam == win32con.MOD_ALT:
                            self.ShowWindow.emit(msg.lParam)
            finally:
                print("success!")

```

> mainwindow.py

```python
import sys, os
from PySide6.QtCore import *
from PySide6.QtWidgets import *
from PySide6.QtGui import *
import hotKey
class UUMainWindow(QWidget):
    ShowWindow = Signal(int)
    def __init__(self, parent=None):
        super(UUMainWindow, self).__init__(parent)
        self.setWindowTitle('主页面')
        self.setGeometry(300, 100, 1300, 800)
    def hot_key_event(self, data):
        if data == 12582913:
            if self.isMinimized():
                self.showNormal()
            else:
                self.showMinimized()
if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = UUMainWindow()
    hot_key = hotKey.HotKey()
    hot_key.ShowWindow.connect(main.hot_key_event)
    hot_key.start()
    main.show()
    sys.exit(app.exec())

```
这样的代码看似完美，运行后可以实现窗口对全局热键的响应，但当第二次按下全局热键时：
![运行截图](https://i-blog.csdnimg.cn/blog_migrate/7f2f62e071983cc7d62a5ae1be400a30.png#pic_center)
于是我又开始在网上寻找解决方案，当我看到了这篇文章（[Qt PySide2实现全局热键(原生)](https://blog.csdn.net/User287/article/details/131932393)）时，一切豁然开朗：**不是success之后就万事大吉了，还要把热键注销，不然下一次就注册不了！！！**
> [!IMPORTANT]
> 还要在`print("success!")`后面加上`user32.UnregisterHotKey(None, 1)`，其中1是hotkey_id。

所以hotKey.py就要改成下面的样子：

> hotKey.py

```python
import win32con
from ctypes import *
from ctypes.wintypes import *
from PySide6.QtCore import *
from PySide6.QtGui import *
from PySide6.QtWidgets import *
import tkinter.messagebox
main_key = 192
class HotKey(QThread):
    ShowWindow = Signal(int)
    def __init__(self):
        super(HotKey, self).__init__()
        self.main_key = 192
    def run(self):
        user32 = windll.user32
        while True:
            if not user32.RegisterHotKey(None, 1, win32con.MOD_ALT, self.main_key):  # alt+~
                tkinter.messagebox.showerror("错误","全局热键注册失败。")
            try:
                msg = MSG()
                if user32.GetMessageA(byref(msg), None, 0, 0) != 0:
                    if msg.message == win32con.WM_HOTKEY:
                        if msg.wParam == win32con.MOD_ALT:
                            self.ShowWindow.emit(msg.lParam)
            finally:
                user32.UnregisterHotKey(None, 1)

```
此时再运行，OK，完美解决！
## 完整DEMO

> hotKey.py

```python
import win32con
from ctypes import *
from ctypes.wintypes import *
from PySide6.QtCore import *
from PySide6.QtGui import *
from PySide6.QtWidgets import *
import tkinter.messagebox
main_key = 192
class HotKey(QThread):
    ShowWindow = Signal(int)
    def __init__(self):
        super(HotKey, self).__init__()
        self.main_key = 192
    def run(self):
        user32 = windll.user32
        while True:
            if not user32.RegisterHotKey(None, 1, win32con.MOD_ALT, self.main_key):  # alt+~
                tkinter.messagebox.showerror("错误","全局热键注册失败。")
            try:
                msg = MSG()
                if user32.GetMessageA(byref(msg), None, 0, 0) != 0:
                    if msg.message == win32con.WM_HOTKEY:
                        if msg.wParam == win32con.MOD_ALT:
                            self.ShowWindow.emit(msg.lParam)
            finally:
                user32.UnregisterHotKey(None, 1)

```

> mainwindow.py

```python
import sys, os
from PySide6.QtCore import *
from PySide6.QtWidgets import *
from PySide6.QtGui import *
import hotKey
class UUMainWindow(QWidget):
    ShowWindow = Signal(int)
    def __init__(self, parent=None):
        super(UUMainWindow, self).__init__(parent)
        self.setWindowTitle('主页面')
        self.setGeometry(300, 100, 1300, 800)
    def hot_key_event(self, data):
        if data == 12582913:
            if self.isMinimized():
                self.showNormal()
            else:
                self.showMinimized()
if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = UUMainWindow()
    hot_key = hotKey.HotKey()
    hot_key.ShowWindow.connect(main.hot_key_event)
    hot_key.start()
    main.show()
    sys.exit(app.exec())

```
> [!NOTE]
> 注册的全局热键是`Alt+~`。
## 总结

 - 抄代码得带上自己的思考，光复制粘贴是没有出路的！
 - 相关项目（[Github地址](https://github.com/sudo0015/Random)）
