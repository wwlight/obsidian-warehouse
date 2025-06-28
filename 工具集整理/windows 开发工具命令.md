#windows #工具 #命令

### [Scoop](https://scoop.sh/) - 适用于 Windows 的命令行安装程序

##### 安装

```bash
# 第一步：设置安装目录
$ $env:SCOOP='D:\DevelopmentApplication\Scoop'
$ [Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')

# 第二步：开启代理，在 powershell 中安装
$ Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
$ iex "& {$(irm get.scoop.sh)} -RunAsAdmin"
```

##### 常用命令

```bash
$ scoop config                        # 查看 Scoop 的配置
$ scoop help                          # 列出所有可用命令
$ scoop search [关键词]                # 在可用的 Bucket 中搜索应用程
$ scoop list                          # 列出所有已安装的软件
$ scoop info [软件名]                  # 显示软件包信息
$ scoop home [软件名]                  # 打开软件包主页
$ scoop install [软件名]               # 安装软件
$ scoop install -g [软件名]            # 全局安装(管理员权限)
$ scoop uninstall [软件名]             # 卸载软件

$ scoop update                        # 更新 Scoop 自身
$ scoop update --all                  # 更新所有应用
$ scoop update [软件名]                # 更新指定应用
$ scoop status                        # 检查可更新的应用
$ scoop hold [软件名]                  # 禁止更新指定应用
$ scoop unhold [软件名]                # 解除禁止更新指定应用

$ scoop cache show                    # 显示缓存
$ scoop cache rm [软件名]              # 删除指定应用缓存
$ scoop cleanup [软件名]               # 清理旧版本

# Bucket 本质上是一个 应用程序清单的仓库，它负责存储和管理应用程序的清单，扩展 Scoop 的应用程序范围，简化软件的安装和更新过程。
$ scoop bucket list                   # 列出已添加的所有 Bucke
$ scoop bucket known                  # 列出所有官方认可的 Bucket
$ scoop bucket add [名称]              # 添加 Bucket
$ scoop bucket rm [名称]               # 删除 Bucket

$ scoop export > ~/Desktop/scoop_backup.json   # 导出已安装 Scoop 应用
$ scoop import ~/Desktop/scoop_backup.json     # 从备份文件恢复所有应用

$ scoop alias list
$ scoop alias add [名称] [命令]         # scoop alias add ls 'scoop list'
$ scoop alias rm [名称]
$ scoop alias show [名称]
```

````ad-summary
title:常用工具下载
collapse: false

```bash
$ scoop install git
$ scoop install winrar
$ scoop install mihomo-party
$ scoop install googlechrome
$ scoop install vscode
$ scoop install hyper
$ scoop install starship
$ scoop install clink
$ scoop install switchhosts
$ scoop install obsidian       # 写作应用程序
$ scoop install gh
$ scoop install gsudo
$ scoop install gping
$ scoop install fnm
$ scoop install fzf
$ scoop install zoxide
$ scoop install nginx
$ scoop install ngrok          # 反向代理，内网穿透
$ scoop install winsw          # 可执行包装程序，起 windows 服务
$ scoop install tlrc           # 控制台命令速查表 tldr-pages
$ scoop install eza            # ls 命令替代品
$ scoop install wechat
$ scoop install webstorm
$ scoop install potplayer      # 万能播放器
$ scoop install keyviz         # 开源按键可视化工具
$ scoop install powertoys      # 自定义 Windows 的实用工具
$ scoop install onefetch
$ scoop install uv             # Python 包和项目管理工具
$ scoop install pyenv

$ scoop install adb
$ scoop install bun
$ scoop install tabby          # SSH 和 Telnet 连接终端
$ scoop install syncthing

# 安装字体
$ scoop bucket add nerd-fonts
$ scoop install LXGWWenKaiMono
$ scoop install FiraCode-NF
$ scoop install FiraCode-NF-Mono
$ scoop install Monaspace-NF
$ scoop install Monaspace-NF-Mono
$ scoop install Maple-Mono-NF-CN
```
````

### 常用 windows 命令

```ad-note
title: 说明
主要在 Powershell 中支持使用
```

##### [netstat](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/netstat)

- (`Network Statistics`) 用于显示网络连接、路由表、接口统计等信息。

```bash
-a  显示所有连接和监听端口
-n  以数字形式显示地址和端口号
-p  显示进程ID/名称（Linux）/协议类型（Windows）
-r  显示路由表
-s  显示每个协议的统计信息

# windows 特有
-o  显示拥有每个连接的进程ID
-b  显示创建每个连接或监听端口的可执行文件

# 查看所有活动连接
$ netstat -ano
# 查看特定端口的占用情况
$ netstat -ano | findstr :80
# 只查看TCP连接
$ netstat -ano -p tcp
# 查看路由表
$ netstat -r
```

##### [tasklist](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/tasklist)

- 显示本地计算机或远程计算机上当前正在运行的进程列表

```bash
$ tasklist /?
$ tasklist | findstr "nginx"
```

##### [taskkill](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/taskkill)

- 结束一个或多个任务或进程。可以按进程 ID 或映像名称来结束进程。

```bash
$ taskkill /?
$ taskkill /F /IM nginx.exe /T
```
