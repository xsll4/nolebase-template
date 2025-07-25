1. 内核
2. Shell
3. 文件系统
4. 应用程序
![300](Pasted%20image%2020250515230924.png)
### 1. 管理进程
### 2. 管理内存
### 3. 管理驱动
### 4. 管理文件和网络
## ......
# Linux Shell
接收用户的命令，经过翻译/转换，交给内核去执行
`cat -> open() read()`
- 我们发送cat等命令,它就调用open和read相关的函数
- shell有自己设计的命令(内部命令),可以去运行/调用别的程序
- 如果我们每个用户都去操作Linux的内核,操作麻烦还不安全,所以我们需要Linux shell(当作Linux的外壳)
**优点:**
  1. 简化操作
  2. 安全
# Linux Shell工具

| 名称                 | 程序路径                  | 作者             |
| ------------------ | --------------------- | -------------- |
| bourne Shell       | /usr/bin/sh或/bin/sh   | Stephen Bourne |
| C Shell            | /usr/bin/csh          | Bill Joy       |
| K Shell            | /usr/bin/ksh          | David Korn     |
| Bourne Again Shell | ==/bin/bash==         | Brian Fox      |
| Z Shell            | /bin/zsh或/usr/bin/zsh | Paul Falstad   |

Windows: cmd、Power Shell
# Shell和Terminal

`Shell`和`Terminal`是在计算机操作中常用的概念。在Unix和类Unix系统（如Linux、macOS）以及Windows的命令提示符等环境中，`Shell`是一个命令行解释器，它接收用户输入的命令并将其传递给操作系统执行，例如`bash`、`zsh`等都是常见的`Shell`。而`Terminal`（终端）则是提供给用户与`Shell`交互的界面，通过图形化界面或文本界面让用户能够输入命令并查看`Shell`执行命令后的输出。

以下是一个简单的在`bash` `Shell`中使用`echo`命令的示例：

```bash
echo "Hello, World!"
```

这段命令会在终端中输出`Hello, World!`。
![400](Pasted%20image%2020250515235227.png)

# Linux文件系统
### “一切皆文件”:
**在Linux中所有的东西都可以通过文件的方式去访问**
普通文件、目录、进程（/proc）、输入输出设备（/dev）、网络字节流socket、链接文件、管道文件

| 查看文件        | 作用                         |
| --------------- | ---------------------------- |
| lsof /bin/bash  | 查找某个文件相关的进程         |
| lsof -u root    | 列出某个用户打开的文件信息     |
| lsof -c redis   | 列出某个程序进程所打开的文件信息 |
| lsof -i tcp     | 列出所有tcp 网络连接信息       |
| ……              | ……                           |

Linux操作系统的文件系统
# 根目录文件-1

| 目录    | 作用                    | 备注                            |
| ----- | --------------------- | ----------------------------- |
| bin   | 存放普通用户可执行的指令          | 即使在单用户模式下也能够执行处理              |
| boot  | 开机引导目录                | 包括Linux内核文件与开机所需要的文件          |
| dev   | 设备目录                  | 所有的硬件设备及周边均放置在这个设备目录中，比如声卡、磁盘 |
| etc   | 各种配置文件目录              | 大部分配置属性均存放在这里                 |
| lib   | 库文件存放地，bin和sbin需要的库文件 | 类似windows的DLL                 |
| media | 可移除设备挂载目录             | 类似U盘、光盘、移动硬盘等临时挂放目录           |
# 根目录文件-2

| 目录   | 作用            | 备注                                                  |
| ---- | ------------- | --------------------------------------------------- |
| mnt  | 用户临时挂载其他的文件系统 | 额外的设备可挂载在这里,相对临时而言                                  |
| opt  | 第三方软件安装目录     | 现在习惯性的放置在`/usr/local`中                              |
| proc | 虚拟文件系统        | 通常是内存中的映射,特别注意在误删除数据文件后,比如DB，只要系统不重启,还是有很大几率能将数据找回来 |
| root | 系统管理员主目录      | 除root之外,其他用户均放置在`/home`目录下                          |
| run  | 系统运行时所需文件     | 以前防止在`/var/run`中,后来拆分成独立的`/run`目录。重启后重新生成对应的目录数据    |
# 根目录文件-3

| 目录 | 作用 | 备注 |
| --- | --- | --- |
| sbin | 只有root才能运行的管理指令 | 跟bin类似,但只属于root管理员 |
| srv | 服务启动后需要访问的数据目录 |  |
| sys | 跟proc一样, 虚拟文件系统 | 记录核心系统硬件信息 |
| tmp | 存放临时文件目录 | 所有用户对该目录均可读写 |
| usr | 应用程序放置目录 |  |
| var | 存放系统执行过程经常改变的文件 |  |
# 用户主目录
主目录: home directory
root用户的主目录是 `/root`
其他用户的主目录是 `/home/用户名`

`cd` 空格 或者 `cd ~`

工作目录: working directory
# 目录指代

| 符号     | 指代                         |
| ------ | -------------------------- |
| 绝对路径   | 由根目录 / 开始写起                |
| 相对路径   | 从当前所在的工作目录开始写起             |
| `/`    | 根目录                        |
| `.`    | 代表当前目录                     |
| `~`    | 代表用户工作目录, `vim ~/.bashrc`  |
| ../    | 代表上一级目录                    |
| ../../ | 上上一级目录, 以此类推, 超出范围的时候代表根目录 |
**在Linux中文件名前带"."是隐藏的**
#### 绝对路径:比如XX省XX市XX区XX街道XX...
#### 相对路径:我在你右手边

