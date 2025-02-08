## 简介
 
Express是一款用于文件同步/复制的桌面应用。为方便同学们拷课件而设计。
 
## 特性
 
### 简洁

- 全新UI，界面简介，重点突出。
- 仅需轻点几下便能同步/复制文件，操作简单。

### 快速

- 独立占用内存，同步/复制速度明显快于文件资源管理器。
 
> [!NOTE]
> 对比Express与文件资源管理器 (单位: MB/s)
> ![Image](https://github.com/user-attachments/assets/c82babe9-fbed-4bcc-a759-14a5622c1b08)

### 高效

- 采用文件同步技术，自动跳过相同文件，并使目标文件夹保持最新。
 
> [!NOTE]
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
Express由`设置`、`启动台`、`U盘扫描`、`U盘弹窗`、`复制/同步窗口`等部分组成，功能如下：

|文件|描述|功能|
|:-|:-|:-|
|ExpressSetting.exe|设置|设置参数；查看日志；打开`帮助`；发送反馈；查看软件及开发者信息|
|ExpressLauncher.exe|启动台|管理`U盘扫描`进程；手动唤出`U盘弹窗`；打开`设置`；打开`帮助`|
|ExpressScan.exe|U盘扫描|后台扫描U盘插入并自动唤出`U盘弹窗`|
|ExpressUsbService.exe|U盘弹窗|打开U盘根目录；选择学科、模式及参数以执行同步/复制|
|ExpressMain.exe|同步/复制窗口|显示当前状态；显示同步/复制进度；查看任务选项|

### 安装

### 设置
#### 导航栏
通过左侧导航栏，可迅速定位到`设置`、`日志`、`帮助`与`关于`页面。
#### 设置
在`设置`中，有`源`、`行为`、`性能`、`存储`、`高级`等5个选项卡组。
- `源`选项卡组
    - `源文件夹`选项卡
    - `云上春晖`选项卡
    - `自定义`选项卡
- `行为`选项卡组
    - `开机时启动`选项卡
    - `完成后通知`选项卡
- `性能`选项卡组
    - `扫描周期`选项卡
    - `并行进程数`选项卡
    - `缓冲区大小`选项卡
- `存储`选项卡组
    - `清除缓存`选项卡
- `高级`选项卡组
    - `恢复默认设置`选项卡
    - `开发者选项`选项卡
    - `帮助`选项卡

#### 日志
打开日志文件夹。
#### 帮助
打开帮助。
#### 关于
- 查看软件及开发者信息。
- 获取帮助。
- 提供反馈。

### 启动台

### U盘扫描

### U盘弹窗

### 同步/复制窗口

### 外观
- Express的外观有深色、浅色两种，并自动跟随系统主题。
- Express的默认主题色为`#7159f9`。

### 日志
Express的日志位于安装目录下的`Log`文件夹中，可通过`设置 > 日志`打开。
> [!TIP]
> Express每同步/复制一个学科文件夹产生一个日志文件，记录了同步/复制的详细信息，详见`FAQ > 日志怎么看？`。

### 配置文件
Express配置文件位于`%appdata%\.Express\config.json`,可以通过`设置 > 开发者选项`打开。
> [!WARNING]
> 配置文件包含Express运行时必要的参数，随意修改可能导致Express无法正常运行。

### 卸载
若要卸载Express，提供以下两种方式：
- 转到`控制面板 > 程序 > 程序和功能 > 卸载程序`，找到`Express`，选择`卸载`。
- 转到Express安装目录，运行`uninstall.exe`。

## FAQ
<details>
<summary>日志怎么看？</summary>
<ul>
<li>
Express每同步/复制一个学科文件夹产生一个日志文件，日志文件的命名格式为
<code class="notranslate">yyyymmdd-hhmmss-n</code>
。
</li>
<li>
在日志文件的第一部分中，
<code class="notranslate">start at</code>
记录了任务开始时间；
<code class="notranslate">Source</code>
记录了源文件夹路径；
<code class="notranslate">DestDir</code>
记录了目标文件夹路径；
<code class="notranslate">Command</code>
记录了模式；
<code class="notranslate">FileLog</code>
记录了日志文件路径
</li>
<li>
接下去的每一行记录了详细的文件增减信息，
<code class="notranslate">+</code>
表示增添新文件，
<code class="notranslate">-</code>
表示删除文件）。
</li>
<li>
在日志文件的最后一部分中，包含此次任务的摘要信息，如发生的错误数及任务结束时间等。
</li>
</ul>
</details>

## 反馈
若在使用过程中发现问题，或希望提出建议，欢迎通过以下方式反馈：
- 转到`设置 > 关于 > 反馈`，点击`发送反馈`；
- 点击[此处链接](https://github.com/sudo0015/Express/issues)，提供反馈。

## 致谢
- **[FastCopy](https://fastcopy.jp/)** (The Fastest Copy Software on Windows, Copyright © FastCopy Lab, LLC.)
- **[PySide6](https://doc.qt.io/qtforpython-6/)** (Qt for Python, Copyright © The Qt Group, GNU Lesser General Public License v.3)

<!--
<details>
<summary>同步原理</summary>

</details>
-->


<!--
> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.
-->
