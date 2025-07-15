# <font color="#245bdb">课程大纲</font>

> [!todo]
> 1. 用户组
> 2. 用户
> 3. 用户管理相关**文件**
> 4. 用户管理基本**命令**
> 5. 文件和目录**归属**
> 6. 文件和目录**权限**
# <font color="#245bdb">用户组Group</font>
==方便权限分配==
![300](Pasted%20image%2020250526222858.png)   ![300](Pasted%20image%2020250526222920.png)
==在Linux中一个用户可以在多个组里,其中有一个组是主要的组,其他都是叫做附属组或者附加组(附加组可以没有,主要组要有)==
# <font color="#245bdb">组ID - Group ID - GID</font>
1. root用户组: `GID = 0`
2. 程序用户组 (系统用户组): 1 - 999 (CentOS7)
3. 普通用户组: 1000 - 65535
`cat /etc/group`
# <font color="#245bdb">Group相关命令</font>

| 操作             | 命令             |
|------------------|------------------|
| 查看全部组       | `cat /etc/group` |
| 查看用户的所属组 | `groups`         |
| 添加用户组       | `groupadd security` |
| 删除用户组       | `groupdel security` |
# <font color="#245bdb">用户ID-User ID-UID</font>

1. `root`用户：`UID=0`<font color="#d83931">（**反之也成立**）</font>
2. 程序用户（系统用户）：`1-999`（CentOS7）
3. 普通用户：`1000-65535`
`cat /etc/passwd`
# <font color="#245bdb">User相关命令</font>

| 操作     | 命令            |
| ------ | ------------- |
| 添加用户   | `useradd ...` |
| 修改用户密码 | `passwd ...`  |
| 删除用户   | `userdel ...` |
| 修改用户信息 | `usermod ...` |
# <font color="#245bdb">/etc/group</font>

1. 组名
2. 组密码
3. GID
4. 用户列表
影子文件:
```bash
cat /etc/gshadow
```

组名: 密码: 组管理员: 组附加用户列表

```
root:x:0:
bin:x:1:
daemon:x:2:
sys:x:3:
adm:x:4:
tty:x:5:
disk:x:6:
lp:x:7:
mem:x:8:
kmem:x:9:
wheel:x:10:
cdrom:x:11:
mail:x:12:postfix
```
# <font color="#245bdb">/etc/passwd</font>
```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
```

1. 用户名
2. 密码
3. UID
4. GID
5. 全名
6. home路径
7. shell工具

`cat /etc/shadow`
# <font color="#245bdb">/etc/shadow</font>

```
wuya:$1$jX8wc27p$bW2rSGQlDCsX2Hz/uwNK70:19157:0:99999:7::::
www:!!:19165:0:99999:7::::
mysql:!!:19173::::::
```

1. 用户名
2. 密码
3. 最后修改时间（1970年1月1日以后的多少天）
4. 最小修改间隔时间
5. 密码有效期
6. 密码需要变更前的警告天数
7. 密码过期后的宽限天数
8. 账号失效时间
9. 保留
# <font color="#245bdb">密码格式</font>
命令: `openssl passwd -1 -salt admin 123456`
格式: `$id$salt$encrypted`
示例: `$1$admin$LClYcRe.ee8dQwgrFc5nz.`
## $+第一位数字的表示:

| 数字 | 加密方式           |
|------|------------------|
| 1    | MD5              |
| 2a   | Blowfish (某些Linux发行版) |
| 5    | SHA-256          |
| 6    | SHA-512          |
==md5可以通过数据库查表的方式破解,所以我们加盐(干扰字符)==
# <font color="#245bdb">/etc/sudoers</font>
==用visudo修改配置文件==
#### 格式:
```
wuya ALL=(ALL) ALL
kali ALL=(ALL) NOPASSWD: /bin/useradd
```
#### 全拼: super user do
```
sudo -l
sudo command (要执行的命令)
```
# <font color="#245bdb">基本命令</font>

| 操作 | 命令 |
| --- | --- |
| 查询用户账号身份标识 | `id` |
| 查询用户账号的登录属性 | `finger` |
| 查询当前主机的用户登录情况 | `w`、`who` |
| 查询系统当前在线的用户 | `users` |
| 查看用户 | `whoami` |
| 切换用户 | `su` |
# <font color="#245bdb">用户和文件的关系</font>
文件所有者：所属用户、所属组
访问权限：读、写、执行
# <font color="#245bdb">文件和目录归属</font>
## 文件的拥有者
## 文件的所属组
## 全拼: change owner
```bash
chown -R wuya /usr/local/soft
chown -R redis:redis /usr/local/soft/redis
```
# <font color="#245bdb">文件类型</font>
![600](Pasted%20image%2020250527230632.png)

| 权限           | 链接数 | 所有者  | 所属组  | 大小   | 日期           | 文件名                                       |
| ------------ | --- | ---- | ---- | ---- | ------------ | ----------------------------------------- |
| `-rw-------` | 1   | root | root | 2750 | Jun 14 14:53 | anaconda-ks.cfg                           |
| `drwxr-xr-x` | 2   | root | root | 6    | Jun 14 06:55 | <span style="color: blue;">Desktop</span> |
![600](Pasted%20image%2020250527230552.png)
### 三段的含义:

| 符号  | 单词    | 含义        |
| --- | ----- | --------- |
| u   | user  | 所属用户（的权限） |
| g   | group | 所属组别（的权限） |
| o   | other | 其他用户（的权限） |
![600](Pasted%20image%2020250527230956.png)

| 符号 | 单词     | 含义   | 对于文件   | 对于目录           |
| ---- | -------- | ------ | ---------- | ------------------ |
| `r`  | `read`   | 可读   | 可以读取   | 可以浏览内容       |
| `w`  | `write`  | 可写   | 可以修改   | 可以删除、移动内容 |
| `x`  | `execute`| 可执行 | 可以执行   | 可以进入目录       |
| `-`  |          | 没有权限 |            |                    |
d: 目录文件 (文件夹)
-: 普通文件
l: 软链接 (类似Windows的快捷方式)
b: 块设备文件 (例如硬盘、光驱等)
p: 管道文件
c: 字符设备文件 (例如屏幕等串口设备)
s: 套接口文
# <font color="#245bdb">权限类别</font> 
![500](Pasted%20image%2020250527232725.png)
# <font color="#245bdb">修改权限</font>
### 添加组用户的写权限。 <font color="#de7802">全拼: change mode</font>
```bash
chmod g+w test.log
```
### 删除其他用户的所有权限。
```bash
chmod o= test.log
  ```
### 使得所有用户都没有写权限。
```bash
chmod a-w test.log
```
### 当前用户具有所有权限, 组用户有读写权限, 其他用户只有读权限。
```bash
chmod u=rwx, g=rw, o=r test.log
```
### 等价的八进制数表示:
```bash
chmod 764 test.log
```
### 将目录以及目录下的文件都设置为所有用户拥有读写权限。
### 注意, 使用'-R'选项一定要保留当前用户的执行和读取权限, 否则会报错!
```bash
chmod -R a=rw testdir/
```
### 根据其他文件的权限设置文件权限。
```bash
chmod --reference=1.log test.log
```

