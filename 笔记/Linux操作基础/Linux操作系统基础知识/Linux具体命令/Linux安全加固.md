# <font color="#245bdb">课程大纲</font>

> [!todo]
> 1. Linux 安全加固概述
> 2. 身份鉴别加固
> 3. 访问控制加固
> 4. 安全审计加固
> 5. 入侵防范加固
> 6. 常见安全产品
> 7. 检测和加固脚本
# <font color="#245bdb">安全加固</font>
- 加固的意义：防患于未然
- 基线检查
  https://help.aliyun.com/document_detail/68386.html
- 加固思路
  GB/T 25070-2019 《信息安全技术 网络安全等级保护安全设计技术要求》
  GB/T 36627-2018 《信息安全技术 网络安全等级保护测试评估技术指南》.pdf
# <font color="#245bdb">用户管理</font>
删除多余、无用账号
```bash
cat /etc/passwd
cat /etc/shadow
```
```bash
userdel xxx
```
# <font color="#245bdb">密码策略-1</font>
## 检查空口令
```awk -F: '($2 == ""){print $1}' /etc/shadow```
```passwd xxx(用户名)```
## 口令有效期
```vim /etc/login.defs```
- `PASS_MAX_DAYS`: 密码最长有效期
- `PASS_MIN_DAYS`: 密码最短有效期
- `PASS_MIN_LEN`: 密码最小强度
- `PASS_WARN_AGE`: 在口令失效前多少天开始通知用户更改密码
# <font color="#245bdb">密码策略-2</font>
## 口令强度
```bash
vim /etc/pam.d/system-auth
```
### 格式:
```bash
password requisite pam_cracklib.so retry=3 difok=2 minlen=8 lcredit=-1 dcredit=-1
```
### 含义:
- `retry`: 重试多少次后返回密码修改错误
- `difok`: 本次密码与上次密码至少不同字符数
- `minlen`: 密码最小长度，此配置优先于`login.def`中的`PASS_MIN_LEN`
- `ucredit`: 最少大写字母
- `lcredit`: 最少小写字母
- `ocredit`: 最少的字符数量
- `dcredit`: 最少数字
# <font color="#245bdb">密码策略-3</font>

## 登录失败策略

### 配置文件路径
```bash
vim /etc/pam.d/sshd
```
### 配置格式
```bash
auth required pam_tally2.so deny=3 unlock_time=300 even_deny_root root_unlock_time=1800
```
### 配置含义
- `even_deny_root`：也限制root用户；
- `deny`：最大次数，则锁定该用户；
- `unlock_time`：设定普通用户锁定后，多少时间后解锁，单位是秒；
- `root_unlock_time`：设定root用户锁定后，多少时间后解锁，单位是秒。
### 解锁命令
```bash
pam_tally2 --user=root --reset
```
# <font color="#245bdb">IP是否允许访问-1</font>
## 允许访问的IP
```bash
vim /etc/hosts.allow
```
```bash
sshd:192.168.142.*:allow #表示192.168.142.* ip段都能ssh访问
sshd:all:allow #表示允许所有ip 的ssh访问
sshd:192.168.142.74:allow #表示允许192.168.142.74ssh访问
```
配置完成后，重启ssh服务
```bash
service sshd restart
```
# <font color="#245bdb">IP是否允许访问-2</font>
## 拒绝访问的IP
```bash
vim /etc/hosts.deny
```
```bash
ssh:dall:deny # 表示拒绝所有ip访问
ssh:47.106.218.*:deny # 表示拒绝47.106.218.* ip段所有ssh访问
ssh:192.168.142.74 # 表示拒绝192.168.142.74 主机ssh访问
```
配置完成后，重启ssh服务
```bash
service sshd restart
```
# <font color="#245bdb">防范端口扫描</font>
## 关闭不必要的端口服务
```bash
systemctl list-unit-files | grep enable
systemctl stop xxx
systemctl disable xxx
```
## 修改默认端口号
例如: `vim /etc/ssh/sshd_config`
## 防火墙策略
`vim /etc/sysconfig/iptables` (需要安装)
```bash
-A INPUT -p tcp --tcp-flags ALL FIN,URG,PSH -j REJECT
-A INPUT -p tcp --tcp-flags SYN,RST SYN,RST -j REJECT
-A INPUT -p tcp --tcp-flags SYN,FIN SYN,FIN -j REJECT
```
# <font color="#245bdb">root权限控制-1</font>
## 禁止root用户远程登录
```bash
vim /etc/ssh/sshd_config
PermitRootLogin no
```
## 禁止其他用户su提权
```bash
vim /etc/pam.d/su
# 只允许wheel组用户
auth sufficient pam_rootok.so
auth required pam_wheel.so group=wheel
```
# <font color="#245bdb">root权限控制-2</font>
## 禁止其他用户sudo提权
`visudo`
## 禁止SUID提权
```bash
ll /usr/bin/passwd(有s权限,普通用户会临时拥有root权限)
find / -user root -perm -4000 -print 2>/dev/null(找有s权限的程序)
chmod ugo-s xxx
```
# <font color="#245bdb">auditd审计</font>
记录文件变化
`/var/log/audit/audit.log`
`ausearch -h`

参考资料:
[](https://docs.oracle.com/zh-cn/learn/ol-auditd/#rules-with-audit-control-utility](https://docs.oracle.com/zh-cn/learn/ol-auditd/#rules-with-audit-control-utility](https://docs.oracle.com/zh-cn/learn/ol-auditd/#rules-with-audit-control-utility)
[http://www.manongjc.com/detail/52-wdjuncovycbmilg.html](http://www.manongjc.com/detail/52-wdjuncovycbmilg.html)
[https://blog.csdn.net/m0_74282605/article/details/128718297](https://blog.csdn.net/m0_74282605/article/details/128718297)
# <font color="#245bdb">更新软件</font>
## 安装更新
`yum check-update` <font color="#00b050"># 列出可更新的软件清单</font>
`yum info updates` <font color="#00b050"># 列出可更新的软件包详细信息</font>
`yum upgrade <package_name>`<font color="#00b050"> # 升级指定软件</font>
`yum updateinfo list updates security` <font color="#00b050"># 列出可用的安全补丁</font>
`yum update` # 升级系统版本和所有软件

`yum --enablerepo=elrepo-kernel install kernel-lt -y` <font color="#00b050"># 更新到最新内核 (需要设置引导)</font>
参考资料:
[https://blog.csdn.net/qq_41632602/article/details/125956150](https://blog.csdn.net/qq_41632602/article/details/125956150)
# <font color="#245bdb">安全产品</font>
## 自动、智能化
## 安全厂商产品概览
## 常见安全产品
  - 主机杀毒、漏洞扫描、防火墙、监控、告警、WAF
  - 堡垒机（运维审计系统）、IPS 入侵防御系统、IDS 入侵检测系统
  - 态势感知、终端安全管理系统EDR、安全管理平台（SCO）
  - 抗DDos、VPN、蜜罐……
- 2022中国网络安全产业全景图（第四版）
  [https://www.freebuf.com/articles/339788.html](https://www.freebuf.com/articles/339788.html
# <font color="#245bdb">加固清单和脚本</font>
## 清单
- linux基线配置文档2.2.docx
## 加固脚本
- `CentOS_Check_Script.sh`
- CentOS_Protective_Script.sh
- linuxcheeklist2.2.sh
# <font color="#245bdb">作业</font>
1. 对各个配置项进行测试验证
2. 整理本节课笔记
3. 如有需要，对相关内容进行拓展学习
