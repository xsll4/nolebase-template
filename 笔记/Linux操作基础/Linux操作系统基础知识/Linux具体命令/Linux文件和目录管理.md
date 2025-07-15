# <font color="#245bdb">课程大纲</font>


> [!todo]
> 1. 列出目录
> 2. 打印工作路径 
> 3. 切换工作路径
> 4. 查看文件类型
> 5. 复制文件或目录
> 6. 查找文件或者目录
> 7. 创建目录
> 8. 移动或者重命名
> 9. 删除文件或目录
> 10. 创建空文件
> 11. 软链接和硬链接
> 12. 挂载

---

## 常规命令格式

## Command Options Arguments
命令 选项 参数
rm    -rf      /*
这个命令的意思是强制删除根目录下的所有文件

> [!hint] 方便理解:
> 命令相当于英语里的动词,选项相当于副词(怎么做/做成什么样),参数相当于名词


> [!解释]
> <font color="#00b050">(-rf为短选项,一个横杠通常会带一个字母,两个横杠通常会带一个单词,这种叫长选项)</font>
> <font color="#00b050">有些命令也不带任何选项和参数<font color="#ff0000">(只有选项和参数是可以省略,命令是绝对不能省)</font></font>
**rm**:remove(删除)
**-rf**:-r(递归的)**+**-f(force:强制的)
### Options选项: 命令的行为方式
### Arguments参数: 命令的对象
## 玩笑:
><font color="#245bdb">Linux怎么</font><font color="#00b050">清理</font><font color="#245bdb">系统</font><font color="#7030a0">垃圾</font><font color="#245bdb">？</font>
>  <font color="#f79646">打开系统Terminal(终端)输入：</font>
> 
>     <font color="#ff0000">sudo</font> <font color="#00b050">rm</font> <font color="#6425d0">-rf</font> <font color="#974806">/</font>*
> 
> - <font color="#ff0000">sudo</font>：以系统管理员的身份执行
> - <font color="#00b050">rm</font>：ReMove 移除
> - <font color="#6425d0">-rf</font>：Rubbish Files 垃圾文件
> - <font color="#974806"> /</font>：目录下
> - `*`：所有文件
> 
> <font color="#ff0000">以系统管理者的身份</font> <font color="#00b050">移除</font>  <font color="#6425d0">Rubbish Flies</font> <font color="#974806">目录下</font> 的所有文件
# <font color="#245bdb">规范</font>
- 命令
- 空格
- 大小写==(Linux区分大小写)==
- 顺序==(大部分情况选项可以变换顺序/拆分/合并不影响结果)==
# <font color="#245bdb">命令选项详细参考资料</font>

- [https://wangchujian.com/linux-command](https://wangchujian.com/linux-command)
- [https://www.linuxcool.com](https://www.linuxcool.com)

---
# <font color="#245bdb">列出目录内容和属性</font>
### 命令: `ls`
### 全拼: `list`
### 格式: `ls` 选项 文件名 
### 例:
```
ls -a
ll --block-size=M
```
# <font color="#245bdb">打印工作路径</font>

命令: `pwd`
全拼: `print working directory`==打印工作路径==
格式: `pwd` 
<font color="#245bdb"># 切换工作目录</font>

**命令**：`cd`
**全拼**：`change directory`
**格式**：`cd` 相对路径或者绝对路径

| 符号 | 指代 |
| --- | --- |
| 绝对路径 | 由根目录 `/` 开始写起 |
| 相对路径 | 从当前所在的工作目录开始写起 |
| `/` | 根目录 |
| `.` | 代表当前目录 |
| `~` | 代表用户工作目录，`vim ~/.bashrc` |
| `../` | 代表上一级目录 |
| `../../` | 上上一级目录，以此类推，超出范围的时候代表根目录 |
# <font color="#245bdb">查看文件类型</font>

命令: `file`
格式: `file 选项 文件或目录`
`file -i 文件名`
==Linux很多文件是没有像Windows一样有文件扩展名的,要查文件格式要用命令file==
# <font color="#245bdb">复制文件或目录</font>
命令: `cp`
全拼: `copy`
格式: `cp` 选项 源文件 目标文件==(复制源文件到目标文件)==
-R/r: 递归处理，将指定目录下的所有文件与子目录一并处理；
-f: 强行复制文件或目录，不论目标文件或目录是否已存在；
> [!tip] 常见选项解释
> -f:force(强制)
> -i:inqure(做什么都要询问一下)
> -v:verbose(详细的)
# <font color="#245bdb">查找文件或者目录-1</font>
## find
格式: find 目录 选项 名字或模式
==(这个目录的意思是在哪里开始找)==
### -name 名字
```
find /etc -name a*
find / -name "aaa" 2>/dev/null
```
1. ==在/ect这个目录下用匹配名字的方式去查找以a开头的文件==
### -type 类型参数
f 普通文件, d 目录
```
find /root -type f
```
# <font color="#245bdb">查找文件或者目录-2</font>

## `size`大小
```bash
find /root -type f -size 10M+
```
## `-exec command`
把`find`找到的内容作为命令的参数去执行
`{}`就是找到的内容
```bash
find. -name "*.txt" -exec rm -rf {} \; （包括子目录）
find. -name aaa -exec mv {} bbb \;
```
1. ==将所有txt文件删除==
# <font color="#245bdb">其他查找命令</font>
whereis：查找二进制程序、代码等相关文件路径
which：查找并显示给定命令的绝对路径
locate：updatedb程序每天会跑一次，建立文件索引
# <font color="#245bdb">创建目录</font>
## 命令: `mkdir`
## 全拼: `make directory`
## 格式: `mkdir 选项 目录名`
`mkdir test`
`mkdir -p /usr/local/soft/redis` 
 ==要建立多级目录必须要加-p(parents)== 
# <font color="#245bdb">移动或者重命名</font>
## 命令: `mv`
## 全拼: `move`
## 格式: `mv` 选项 原文件 新文件
```bash
mv 1.txt 2.txt
mv /a/1.txt /b/1.txt
```
# <font color="#245bdb">删除文件</font>
**命令:** `rm`
**全拼:** `remove`
**格式:** `rm 选项 (多个)文件名`
删除空目录: `rmdir`
- `-r` 递归 (连同子文件夹一起删除)
- `-f` 强制删除
`find . -name "a.json" -exec rm -rf {}`
# <font color="#245bdb">创建空文件</font>
命令: `touch`
格式: `touch 选项 文件名`
`touch a.txt`
==(如果一个文件已经存在,就会更新它的一个时间戳)==

---
# 挂载和链接
# <font color="#245bdb">挂载mount</font>

## 问题: 一个目录树怎么使用多个磁盘?

原路径: `/dev/sdb1` 挂载到: `/sdb-u`
```bash
mkdir /sdb-u
mount /dev/sdb1 /sdb-u
```
1. 先创建一个文件夹
2. 然后挂载在目标目录下
![400](Pasted%20image%2020250520010914.png)
a) Linux 系统文件目录（一部分）   b) U盘文件系统目录
# <font color="#245bdb">挂载mount</font>
挂载后:
![340](Pasted%20image%2020250520204352.png)
# <font color="#245bdb">链接</font>
## 命令`ln`
## 全拼:`link`
## 格式`ln 源文件 链接文件`
### 创建硬链接
```bash
ln 1.php hard.php
vim hard.php
cat 1.php
```
## 注意
1. **用户**不能给**目录**创建**硬**链接==(只有操作系统才能给目录创造硬链接)==
2. 只有相同的文件系统才可以创建硬链接 (tmpfs NTFS FAT32)
# <font color="#245bdb">软链接</font>

查看软链接:
```
ll /usr/bin/nc
```
创建软链接:
```
ln -s /usr/local/phpstudy/system/phpstudyctl /usr/bin/study
```
使用:
```
study
```

源文件删除, 软连接失效
