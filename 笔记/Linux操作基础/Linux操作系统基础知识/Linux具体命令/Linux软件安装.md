# <font color="#245bdb">课程大纲</font>

> [!todo]
> 1. 软件为什么需要安装
> 2. 脚本和程序的区别
> 3. Linux安装软件的几种方式
> 4. CentOS安装软件案例
> 5. Linux软件版本管理
# <font color="#245bdb">Windows软件安装流程</font>
1. 安装检查
2. 释放文件
3. 复制可执行文件
4. DLL动态链接库/安装服务
5. 注册表
6. 开始菜单和快捷方式
# <font color="#245bdb">Windows安装文件</font>
![500](Pasted%20image%2020250525182559.png)
# <font color="#245bdb">Windows可执行程序</font>
![400](Pasted%20image%2020250525182823.png)
# <font color="#245bdb">Linux可执行程序</font>
- `/bin`
- `/sbin`
- `/usr/bin`
- `/usr/sbin`
==在Linux操作系统里并没有像Windows那样有对文件扩展名的要求,它通过文件头来识别文件的,只要可执行权限就可以==
# <font color="#245bdb">脚本和程序的区别</font>
不需要编译的：Javascript、Python、Ruby……
需要编译的：C、C++、Swift、Kotlin、Go……
解释型：边解释边执行
编译型：计算机可以直接执行
==脚本语言性能弱一些但是跨平台能力更强==
==Java介于这两者之间,编译成class文件还要用Java虚拟机再次编译,各个平台有各个平台的虚拟机==
# <font color="#245bdb">Linux软件常见安装方式</font>
源码编译（make）、rpm、deb、yum、apt、Docker……
# <font color="#245bdb">Linux主要派系</font>

| 主要派系       | Linux发型版              | 主要安装方式           |
| ---------- | --------------------- | ---------------- |
| Redhat红帽派系 | Redhat、CentOS、Fedora等 | make、rpm、yum、dnf |
| Debian派系   | Kali、Ubuntu等          | deb、apt、dpkg     |
| FreeBSD系   | FreeBSD               | make、pkg、ports   |
# <font color="#245bdb">源码安装</font>

### 下载源代码安装包文件
### 步骤1: tar包解压缩
用途: 解压并释放源代码包到指定的目录
### 步骤2: ./configure配置
用途: 设置安装目录、安装模块等选项
### 步骤3: make编译
用途: 生成可执行的二进制文件
### 步骤4: make install
用途: 复制二进制文件到系统, 配置环境
### 配置并使用软件
案例 (教程合集):
- 41-CentOS7安装Redis 6.pdf
- 42-CentOS7源码方式安装nginx.pdf
# <font color="#245bdb">rpm安装</font>
RedHat Package Manager
![350](Pasted%20image%2020250526190249.png)
==rpm已经包含了编译好的程序,不用去手动编译==
# <font color="#245bdb">rpm选项</font>

| 操作  | 命令                       | 说明                                  |
| --- | ------------------------ | ----------------------------------- |
| 查询  | `rpm -qa`<br>`rpm -q 包名` | q: query                            |
| 安装  | `rpm -ivh 包名`            | i: install<br>v: verbose<br>h: hash |
| 升级  | `rpm -Uvh 包名`            | U: 安装或升级最新版                         |
| 卸载  | `rpm -e 包名`              | 需要先卸载依赖其的软件                         |
==rpm不能解决软件依赖的问题,有可能你为了下载一个软件就下载了一堆rpm,非常麻烦==
# <font color="#245bdb">yum安装</font>
YUM (Yellow dog Updater, Modified)
案例（教程合集）：
- 06-CentOS7 yum方式安装Docker
- 43-CentOS7 yum方式安装MySQL 5
==yum解决了软件依赖关系(基于rpm,主动去找rpm的包,不是rpm的替代品)的问题==
# <font color="#245bdb">yum操作和选项</font>

## 操作与命令
| 操作      | 命令                                       |
| ------- | ---------------------------------------- |
| 列表      | `yum list`<br>`yum list 包名`              |
| 搜索      | `yum search 包名`                          |
| 安装      | `yum install 包名`                         |
| 升级      | `yum update 包名`                          |
| 卸载      | `yum remove 包名`                          |
| 更新所有软件  | `yum update`                             |
| 清除缓存    | `yum clean all`                          |
| 更新yum缓存 | `yum make cache`==(把远程服务器最新的软件清单拉一份下来)== |

## 选项与含义
| 选项 | 含义 |
| --- | --- |
| `-h` | 显示帮助信息 |
| `-y` | 对所有的提问都回答 "yes" |
| `-c` | 指定配置文件 |
| `-q` | 安静模式 |
| `-v` | 详细模式 |
# <font color="#245bdb">DNF和YUM的区别</font>

## DNF（Dandified YUM）

| 区别 | DNF | YUM |
| --- | --- | --- |
| 解析依赖关系 | 使用Libsolv | 使用公开的API |
| API | 有完整的API文档，能很容易地创建新功能 | 没有完整文档，创建新功能困难 |
| 开发语言 | C、C++、Python编写 | 只用Python编写 |
| 使用范围 | Fedora、RHEL 8、CentOS 8、OEL 8、Mageia 6/7 | RHEL 6/7、CentOS 6/7、OEL 6/7 |
| 扩展的支持 | 支持各种扩展 | 只支持基于Python的扩展 |
| 同步元数据 | 占用内存少 | 占用较多内存 |
| 更新 | 包中包含不相关的依赖，则不会更新 | 在没有验证的情况下更新软件包 |
| 存储库不可用 | DNF将跳过它，并继续使用可用的存储库处理事务 | YUM会立即停止 |
| 内核包的保护 | DNF不提供，可以删除内核包 | 不允许你删除运行中的内核 |
# <font color="#245bdb">Debian系</font>
## Deb包安装 
## apt安装==(有了apt,就不用deb了)==

| 操作 | 命令 |
| --- | --- |
| 搜索 | `apt search 包名` |
| 安装 | `apt install 包名` |
| 升级 | `apt update 包名` |
| 卸载 | `apt remove 包名` |
# <font color="#245bdb">FreeBSD系</font>
## package
## ports

| 操作 | 命令 |
| --- | --- |
| 搜索 | `pkg search 包名` |
| 安装 | `pkg install 包名` |
| 升级 | `pkg upgrade 包名` |
| 卸载 | `pkg del 包名` |
# <font color="#245bdb">Linux软件安装方式</font>

## CentOS启用中文输入法

## CentOS yum安装MySQL
# <font color="#245bdb">update-alternatives</font>

## 查看
```
update-alternatives --display java
```
## 添加
```
alternatives --install /usr/bin/java java /usr/local/jdk-11.0.2/bin/java 3
```
- <font color="#ff0000">/usr/bin/java: 注册地址，软链</font>
- <font color="#00b0f0">java: 服务名</font>
- <font color="#0070c0">/usr/local/jdk-11.0.2/bin/java: 实际程序路径</font>
- <font color="#ffc000">3: 优先级</font>
## 切换
```
update-alternatives --config java
```
