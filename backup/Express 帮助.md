## 简介
 
Express 是一款用于文件同步/复制的桌面应用。为方便同学们拷课件而设计。
 
## 特性
 
### 简洁

- 全新UI，界面简介，重点突出
- 仅需轻点几下便能同步/复制文件，操作简单。

### 快速

- 独立占用内存，同步/复制速度明显快于文件资源管理器。
 
> [!NOTE]
> 对比FastCopy与文件资源管理器 (单位: MB/s)[^1]
> 
> ![Image](https://github.com/user-attachments/assets/27d2be24-e750-4085-948e-13382ecc1034)

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

## 常见问题

## 反馈

## 致谢
- **[FastCopy](https://fastcopy.jp/)** (The Fastest Copy Software on Windows, Copyright © FastCopy Lab, LLC.)
- **[PySide6](https://doc.qt.io/qtforpython-6/)** (Qt for Python, Copyright © The Qt Group, GNU Lesser General Public License v.3)

[^1]: 数据来自网络。
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