# <font color="#245bdb">文本编辑器</font>
Windows: Notepad（记事本）、Sublime、UltraEdit等
Linux: VI/VIM、nano、Emacs、Sed、gedit、Kate等
# <font color="#245bdb">课程大纲</font>

> [!todo]
> 1. VI和VIM的区别
> 2. VIM配置文件
> 3. VIM三种模式的关系
> 4. 命令模式
> 5. 编辑模式
> 6. 底行模式
# <font color="#245bdb">VI和VIM的区别</font>
- VI: Visual Interface
- 1976 Bill Joy(ex)
- 1991 Bram Moolenaar
- Vim: VI IMproved==(代码开发工具)==
==vim兼容vi的所有命令,是vi的进阶提升版, 大部分情况使用vim==
==vim支持的操作系统多==
# <font color="#245bdb">VIM配置文件</font>
### 全局配置: `/etc/vimrc`
### 用户配置: `~/.vimrc`
详细配置参考:
[https://blog.csdn.net/xiao_yi_xiao/article/details/118491698](https://blog.csdn.net/xiao_yi_xiao/article/details/118491698)
# <font color="#245bdb">VIM三种模式区别</font>
## 命令模式:通过命令操作文本文件
## 编辑模式:对文本的内容进行编辑
## 底行模式:结束操作的时候使用
# <font color="#245bdb">VIM三种模式切换</font>
![300](Pasted%20image%2020250524155338.png)
# <font color="#245bdb">打开文件</font>

## VIM 文件名
```
vim /etc/sysconfig/network-scripts/ifcfg-ens33
vim redis.conf
```
### 错误提示:
E325: ATTENTION
<font color="#ff0000">**Found a swap file**</font> by the name ".redis.conf.swp"
### 原因: 编辑未结束
### 解决办法: 保存文本文件, 或者删除.swp
# <font color="#245bdb">移动光标操作</font>

| 操作               | 按键          |
| ---------------- | ----------- |
| 移动光标             | 方向键↑↓←→     |
| 跳到行首             | HOME        |
| 跳到行尾             | END         |
| 向后前进多少行          | n+数字        |
| 退出前进一屏 (Forward) | Ctrl+F      |
| 后退一屏 (Backspace) | Ctrl+B      |
| 跳到文档末尾           | Shift+G / G |
| 跳到文档开头           | :1 / gg     |
# <font color="#245bdb">搜索替换操作</font>

| 操作     | 按键         |
| ------ | ---------- |
| 向后查找内容 | `/关键字, 回车` |
| 向前查找内容 | `?关键字, 回车` |
| `n`    | `下一个关键字`   |
| `N`    | `上一个关键字`   |
# <font color="#245bdb">删除和复制操作</font>

| 操作 | 按键 |
| --- | --- |
| 复制光标所在行 | `yy` |
| 粘贴到下一行/上一行 | `p/P` |
| 删除光标前面一个字符 | `X` |
| 删除光标后面1个字符 | `Del/x` |
| 删除一行 | `dd` |
| 删除光标下面n行 | `ndd` |
| 重复上一次的操作 | `.` |
| 撤消最近一次操作 | `u` |
| 恢复最近一次操作 | `Ctrl+R` |
# <font color="#245bdb">进入编辑模式</font>
a：在光标下一个字符之前插入文本
A：在光标所在的航模插入文本
<font color="#ff0000">i：在光标上一个字符之前插入文本</font>
l：光标的行首插入文本
o：在光标所在的行下插入一行文本
O：在光标所在的行上插入一行文本
r：修改当前光标所在的字符
R：替换文本
# <font color="#245bdb">撤销</font>
编辑模式下：`Ctrl+U` 撤销
退出编辑模式：`Esc`
# <font color="#245bdb">进入底行模式</font>

### `Shift + :`
- `:w` 保存
- `:q` 退出
- `:wq` 保存并且退出
- `:q!` 放弃修改，退出
- `:e!` 放弃所有更改，重新编辑（不关闭）
### 显示行号：`:set nu`==(这是一个临时命令,如果要每次打开都有行号,需要去改命令的配置文件/etc/vimrc)==
### `:%s/word1/word2/g` 把文档中的`word1`替换为`word2`