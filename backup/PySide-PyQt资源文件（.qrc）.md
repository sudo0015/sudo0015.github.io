关于这个资源文件的配置，很多资料说用先用Qt Creator写qrc文件，再转成py文件。个人觉得没有这个必要，参考了一下[官网的教程](https://doc.qt.io/qtforpython-6/tutorials/basictutorial/qrcfiles.html)，这里做一个整理。
## 创建.qrc文件
 新建一个文本文档，把下面的玩意粘贴进去，再把后缀改成qrc。

```html
<!DOCTYPE RCC><RCC version="1.0">
<qresource prefix="/">
   <file>icon.png</file>
   <file>manual.pdf</file>
</qresource>
</RCC>
```

> [!TIP]
>icon.png和manual.pdf换成自己想添加的文件（注意要在同一目录下），你也可以添加更多文件。
>prefix是前缀，这里不建议改成别的。
## 转成.py文件
在cmd中打开刚才目录的位置（用cd命令或者在文件资源管理器中打开，地址栏输入cmd回车），输入

```bash
pyside6-rcc 文件名.qrc -o 文件名.py
```
> [!NOTE]
> `pyside6-rcc`实际上就是`rcc -g python`。
## 引用
 之后`import 文件名.py`，在主程序中用`":/icon.png"`就能定位到资源，比如设置窗口图标，写法如下：

```python
self.setWindowIcon(QIcon(":/icon.png")) 
```

