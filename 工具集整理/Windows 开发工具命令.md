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
$ scoop config                     # 查看 Scoop 的配置
$ scoop help                       # 列出所有可用命令
$ scoop search [关键词]             # 在可用的 Bucket 中搜索应用程
$ scoop list                       # 列出所有已安装的软件
$ scoop info [软件名]               # 显示软件包信息
$ scoop home [软件名]               # 打开软件包主页
$ scoop install [软件名]            # 安装软件
$ scoop install -g [软件名]         # 全局安装(管理员权限)
$ scoop uninstall [软件名]          # 卸载软件

$ scoop update                     # 更新 Scoop 自身
$ scoop update *                   # 更新所有应用
$ scoop update [软件名]             # 更新指定应用
$ scoop status                     # 检查可更新的应用
$ scoop hold [软件名]               # 禁止更新指定应用
$ scoop unhold [软件名]             # 解除禁止更新指定应用

$ scoop cache show                 # 显示缓存
$ scoop cache rm [软件名]           # 删除指定应用缓存
$ scoop cleanup [软件名]            # 清理旧版本

# Bucket 本质上是一个 应用程序清单的仓库，它负责存储和管理应用程序的清单，扩展 Scoop 的应用程序范围，简化软件的安装和更新过程。
$ scoop bucket list                # 列出已添加的所有 Bucke
$ scoop bucket update              # 更新所有已添加的 Bucket
$ scoop bucket known               # 列出所有官方认可的 Bucket
$ scoop bucket add [name]          # 添加 Bucket
$ scoop bucket rm [name]           # 删除 Bucket

# 导出已安装 Scoop 应用
$ scoop export > scoop_backup.json
# 从备份文件恢复所有应用
$ scoop import scoop_backup.json

$ scoop alias list
$ scoop alias add [名称] [命令]
# scoop alias add ls 'scoop list'
$ scoop alias rm [名称]
$ scoop alias show [名称]
```

### 常用 windows 命令

```ad-note
title: 说明
主要在 Powershell 中支持使用
```

##### tasklist

- 显示本地计算机或远程计算机上当前正在运行的进程列表

```bash
$ tasklist /?
$ tasklist | findstr "nginx"
```

##### taskkill

- 结束一个或多个任务或进程。可以按进程 ID 或映像名称来结束进程。

```bash
$ taskkill /?
$ taskkill /F /IM nginx.exe /T
```
