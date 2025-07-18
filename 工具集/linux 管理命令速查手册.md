```sh
# --------------------------
# 1. 用户管理
# --------------------------

# 查看当前用户
whoami

# 查看用户信息
id
id username

# 查看所有用户
cat /etc/passwd

# 添加用户
sudo useradd username
sudo passwd username  # 设置密码

# 删除用户
sudo userdel username          # 保留主目录
sudo userdel -r username       # 删除用户及主目录

# 修改用户信息
sudo usermod -aG groupname username  # 将用户添加到组
sudo usermod -s /bin/bash username   # 修改默认shell
sudo usermod -d /new/home username   # 修改主目录

# 切换用户
su - username      # 完全切换(加载环境变量)
su username        # 仅切换身份

# --------------------------
# 2. 组管理
# --------------------------

# 查看组信息
groups username    # 查看用户所属组
getent group       # 查看所有组
getent group groupname  # 查看特定组

# 添加组
sudo groupadd groupname

# 删除组
sudo groupdel groupname

# 管理组成员
sudo gpasswd -a username groupname  # 添加用户到组
sudo gpasswd -d username groupname  # 从组移除用户

# --------------------------
# 3. 密码管理
# --------------------------

# 修改密码
passwd           # 修改当前用户密码
sudo passwd username  # root修改其他用户密码

# 锁定/解锁账户
sudo passwd -l username  # 锁定
sudo passwd -u username  # 解锁

# --------------------------
# 4. 进程管理
# --------------------------

# 查看用户进程
ps -u username
pgrep -u username

# 终止用户所有进程
sudo pkill -9 -u username
sudo killall -u username

# --------------------------
# 5. 文件权限检查
# --------------------------

# 查找用户/组拥有的文件
sudo find / -user username 2>/dev/null
sudo find / -group groupname 2>/dev/null

# 修改文件属主/组
sudo chown username:groupname file
sudo chown username file      # 仅修改属主
sudo chgrp groupname file     # 仅修改属组

# --------------------------
# 6. 日志与审计
# --------------------------

# 查看用户登录记录
last
lastlog

# 查看sudo记录
sudo cat /var/log/auth.log | grep sudo
```
