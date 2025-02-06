## 简介
 
Express 是一款用于文件同步/复制的桌面应用。为方便同学们拷课件而设计。
 
## 特性
 
### 简洁

- 全新UI，界面简介，重点突出。
- 仅需轻点几下便能同步/复制文件，操作简单。

### 快速

- 独立占用内存，同步/复制速度明显快于文件资源管理器。
 
> [!NOTE]
> 对比`FastCopy`与`文件资源管理器` (单位: MB/s)[^1]
> 
> ![Image](https://github.com/user-attachments/assets/27d2be24-e750-4085-948e-13382ecc1034)
> *注：数据来自网络。*

### 高效

- 采用文件同步技术，自动跳过相同文件，并使目标文件夹保持最新。
 
> [!TIP]
> 同步原理
>
> |源文件夹|目标文件夹|操作|
> |:-:|:-:|:-:|
> |存在|存在|跳过|
> |存在|不存在|复制|
> |不存在|存在|删除|
>
> *注：通过比较源文件夹与目标文件夹，同步能够始终保持两个文件夹完全相同。*

### 可靠

- 内嵌文件校验，保证目标文件夹与源文件夹完全一致。
 
## 开始使用

### 概述
Express由`设置`、`启动台`、`U盘扫描`、`U盘弹窗`、`复制/同步窗口`、`帮助`等部分组成，功能如下：

|文件|描述|功能|
|:-|:-|:-|
|ExpressSetting.exe|设置|设置参数；查看日志；打开`帮助`；发送反馈；查看软件及开发者信息|
|ExpressLauncher.exe|启动台|管理`U盘扫描`进程；手动唤出`U盘弹窗`；打开`设置`；打开`帮助`|
|ExpressScan.exe|U盘扫描|后台扫描U盘插入并自动唤出`U盘弹窗`|
|ExpressUsbService.exe|U盘弹窗|打开U盘根目录；选择学科、模式及参数以执行同步/复制|
|ExpressMain.exe|同步/复制窗口|显示当前状态；显示同步/复制进度；查看任务选项|
|ExpressHelp.exe|帮助|打包为应用程序的[HTML网页](https://sudo0015.github.io/post/Express%20-bang-zhu.html)，查看帮助|

### 安装

### 设置

### 启动台

### U盘扫描

### U盘弹窗

### 同步/复制窗口

### 外观
- Express的外观有深色、浅色两种，并自动跟随系统主题。
- Express的默认主题色为`#7159f9`，可在配置文件中修改，详见……

### 配置文件
Express配置文件位于`%appdata%\.Express\config.json`,可以通过`设置 > 开发者选项`打开。
> [!WARNING]
> 配置文件包含Express运行时必要的参数，随意修改可能导致Express无法正常运行。

### 卸载
若要卸载Express，提供以下两种方式：
- 转到`控制面板 > 程序 > 程序和功能 > 卸载程序`，找到`Express`，选择`卸载`。
- 转到Express安装目录，运行`uninstall.exe`。

## FAQ

## 反馈
若在使用过程中发现问题，或希望提出建议，欢迎通过以下方式反馈：
- 转到`设置 > 关于 > 反馈`，点击`发送反馈`；
- 点击[链接](https://github.com/sudo0015/Express/issues)，提供反馈。

## 致谢
- **[FastCopy](https://fastcopy.jp/)** (The Fastest Copy Software on Windows, Copyright © FastCopy Lab, LLC.)
- **[PySide6](https://doc.qt.io/qtforpython-6/)** (Qt for Python, Copyright © The Qt Group, GNU Lesser General Public License v.3)
