# <font color="#245bdb">课程大纲</font>

> [!todo]
> 1. 查看系统信息
> 2. 进程管理
> 3. 内存使用情况
> 4. 磁盘使用情况
> 5. 定时任务
# <font color="#245bdb">查看系统信息</font>
## 1、日期时间
- `date`
- `cal`
- `uptime`==(开机了多长时间)==
- `w`
## 2、系统版本
- `cat /etc/redhat-release`
- `uname -a`
- `cat /proc/version`
# <font color="#245bdb">程序、进程、服务</font>
1. 程序 program==(静态的描述)==
2. 进程 process==(有状态的,运行起来的代码,一个程序可以运行多个进程)(有唯一的process id)(父进程和子进程)==
3. 服务 service==(注册在操作系统)==
```bash
systemctl list-unit-files | grep mysql
cat /etc/services | grep mysql
```
# <font color="#245bdb">运行程序</font>
1. 前台运行 `./xxx`==(会打印日志,屏幕不断滚动)==
2. 后台运行 `nohup ./xxx &`
# <font color="#245bdb">查看进程 top</font>
![700](Pasted%20image%2020250531160242.png)
==用户有什么权限启动的进程就有什么权限==
# <font color="#245bdb">ps</font>
## 全拼: process status

| 选项   | 作用                        |
| ---- | ------------------------- |
| `-a` | 显示所有进程，包括其他用户的进程；         |
| `-u` | 选择有效的用户id或者是用户名；          |
| `-x` | 显示没有控制终端的进程，同时显示各个命令的具体路径 |
| `-e` | 显示所有的进程，和 `-A` 的效果一样；     |
| `-f` | 显示更完整；通常与 `-e` 一起用；       |

# <font color="#245bdb">ps -ef</font>
![600](Pasted%20image%2020250531161138.png)
# <font color="#245bdb">ps -aux</font>
![600](Pasted%20image%2020250531161326.png)
# <font color="#245bdb">pstree</font>
==(进程树)==
```
pstree -p
pstree mysql(用户名)
pstree -p | grep ssh
```
# <font color="#245bdb">服务管理</font>
## systemctl

| 命令                          | 作用           |
|-------------------------------|----------------|
| `systemctl status *.service`    | 查看所有服务状态 |
| `systemctl start mysqld.service`| 启动服务       |
| `systemctl restart mysqld.service`| 重启服务       |
| `systemctl stop mysqld.service` | 停止服务       |
| `systemctl enable mysqld.service`| 开机启动服务   |
| `systemctl disable mysqld.service`| 停止开机启动   |
# <font color="#245bdb">systemctl和service</font>

| daemon命令             | systemctl命令                   |
| -------------------- | ----------------------------- |
| service [服务] start   | systemctl start [unit type]   |
| service [服务] stop    | systemctl stop [unit type]    |
| service [服务] restart | systemctl restart [unit type] |
# <font color="#245bdb">停止程序</font>

| 信号量 | 含义   | 服务停止                                               |
| --- | ---- | -------------------------------------------------- |
| 0   | EXIT | 程序退出时收到该信息                                         |
| 1   | HUP  | 挂掉电话线或终端连接的挂起信号，这个信号也会造成某些进程在没有终止的情况下重新初始化         |
| 2   | INT  | 表示结束进程，但并不是强制性的，常用的 "Ctrl+C" 组合键发出就是一个 kill -2 的信号 |
| 3   | QUIT | 退出                                                 |
| 9   | KILL | 杀死进程，即强制结束进程                                       |
| 11  | SEGV | 段错误                                                |
| 15  | TERM | 正常结束进程，是 kill 命令的默认信号                              |
# <font color="#245bdb">free</font>
`free`
`free -h`==(可读)==
`free -m`==(只用兆为单位)==
![700](Pasted%20image%2020250531164105.png)
# <font color="#245bdb">磁盘使用情况</font>
`du`
全拼: disk usage
```dataviewjs  
// 定义表头
const headers = ["命令", "作用"];
// 定义数据行（基于你提供的表格，仅提取命令和作用列）
const data = [
  ["`du /usr`", "显示使用情况"],
  ["`du -h /usr`", "`--human-readable`用恰当的单位"],
  ["`du -h /root --max-depth=1`", "加上层级限制"],
  ["`du -h --max-depth=1 | sort -hr`", "降序排列"],
  ["`du -ah /root | sort -hr | head -n 3`", "前三个大文件"],
  ["`du -ah --exclude=\"*/.*\" .`", "排除隐藏目录"], // 双引号已转义
  ["`du -kt 10M ./*`", "找出10M以上的文件"]
];
// 渲染表格
dv.table(headers, data);
```  
# <font color="#245bdb">综合命令 sar</font>
全拼: system activity reporter==(系统活动情况报告)==
`%user`: 用于表示用户模式下消耗的 CPU 时间的比例;
`%nice`: 通过 nice 改变了进程调度优先级的进程, 在用户模式下消耗的 CPU 时间的比例;
`%system`: 系统模式下消耗的 CPU 时间的比例;
`%iowait`: CPU 等待磁盘 I/O 导致空闲状态消耗的时间比例;
`%steal`: 利用 Xen 等操作系统虚拟化技术, 等待其它虚拟 CPU 计算占用的时间比例;
`%idle`: CPU 空闲时间比例。
# <font color="#245bdb">定时任务</font>
工具: crontab
全拼: cron table
Cron表达式:
https://tool.lu/crontab
# <font color="#245bdb">crontab命令</font>

| 命令                        | 作用            |
| ------------------------- | ------------- |
| crontab -u root -r        | 删除任务remove    |
| crontab -u root time.cron | 把文件添加到某个用户的任务 |
| crontab -u root -l        | 列举任务list      |
| crontab -u root -e        | 编辑任务edit      |

## 示例脚本:
test.cron 输出wuya666
time.cron 打印时间
# <font color="#245bdb">定时任务文件</font>

| 命令           | 作用                           |
| -------------- | ------------------------------ |
| `/etc/crontab`   | 管理文件                       |
| `/var/spool/cron/` | 每个用户包括root的cron任务       |
| `/etc/cron.d/`   | 存放任何要执行的cron文件或脚本     |
