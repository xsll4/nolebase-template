# 命令帮助

## ==man== command (manual)—— 具体参数和使用方法
## whatis command —— 命令的简要说明
## info command —— 详细介绍
## help command —— Linux 内置命令

在线查询:
- [https://wangchujiang.com/linux-command](https://wangchujiang.com/linux-command)
- [https://www.linuxcool.com](https://www.linuxcool.com)
# 关机重启(root用户)

## 关机:
- `poweroff`
- `shutdown -h now`
- `halt -p`
## 重启:
- `reboot`
# 快捷键和命令-1

| 操作             | 作用             |
| -------------- | -------------- |
| Tab键           | 补全命令和目录（自动提示）  |
| 方向键            | 上一条命令：↑；下一条命令↓ |
| Ctrl + Insert  | 复制             |
| Shift + Insert | 粘贴             |
| Alt + Insert   | 复制并粘贴          |
| Ctrl+E         | 光标移动到行尾        |
| Ctrl+A         | 光标移动到行首        |
| Ctrl+K         | 清除光标后至行尾的内容    |
| Ctrl+U         | 清除光标前至行首间的所有内容 |
# 快捷键和命令-2

| 操作           | 作用                                                                 |
| ------------ | ------------------------------------------------------------------ |
| `Ctrl + r`   | 搜索历史命令，回车执行                                                        |
| `!cd:`       | 重复执行最近一次，以 cd 开头的历史命令                                              |
| `clear`      | 清屏；向上滚动屏幕，命令还在                                                     |
| `history`    | 查看历史命令                                                             |
| `history -c` | 清除历史命令（新建会话以后还在）                                                   |
| 彻底清除历史命令     | centos: `echo > ~/.bash_history`<br>kali: ` echo > ~/.zsh_history` |
# 通配符

| 符号   | 指代                          |
| ---- | --------------------------- |
| `*`  | 任意字符                        |
| `?`  | 单个字符                        |
| `[]` | 匹配范围中的，比如`[0-9][a-z]`       |
| `{}` | 多个 ，如`ll {*.log,*.txt}`     |
| `^`  | 取反，如`ll *[^txt]` 查找不是.txt结尾 |
# 系统环境变量
告诉操作系统找一个程序去哪里找,在系统环境变量编辑器里的path中去配置可运行程序的路径
环境变量的作用?
查看全部变量: `env`
查看单个变量: `echo $XXX`
用户变量: `~/.bashrc`
系统变量: `/etc/profile`
# 案例: 设置JDK环境变量

```bash
vim /etc/profile
export JAVA_HOME=/usr/local/soft/java/jdk1.8.0_74
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

读取文件并执行命令: `source /etc/profile`