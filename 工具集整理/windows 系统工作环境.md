#windows #安装 #命令

```ad-info
title: 说明
工欲善其事，必先利其器。
```

### ℹ️ 说明

- ✅：免费｜推荐
- ❎：收费｜了解｜科学

### 🍀 准备工作

- 🗂️ 创建文件夹：`DevelopApplication`、`SystemApplication`

```bash
# -p 自动创建父目录
$ mkdir -p D:/{DevelopApplication,SystemApplication}
$ mkdir -p ~/.zsh/{plugins,cache,functions,zfunc}
$ mkdir -p ~/.config/starship
$ mkdir -p ~/.npm_global
```

- ❎️ [Ghelper](https://ghelper.net/) - 浏览器插件 | [极简插件](https://chrome.zzzmh.cn/)
- ✅ [Scoop](https://scoop.sh/) - 适用于 Windows 的命令行安装程序
- ✅ [Nerd Fonts](https://www.nerdfonts.com/font-downloads) - 为开发者提供**图标字体**补丁

### ⭐ 同步配置

- ✅ [wwlight/use](https://github.com/wwlight/use)

### ✍🏻 终端配置

- ✅ [zsh](https://www.zsh.org/) - 功能强大的 shell
	- 将 [zsh 安装包](https://packages.msys2.org/packages/zsh?repo=msys&variant=x86_64) 解压到 git 的安装根目录下
	- Zsh plugins：
		- [zdharma-continuum/fast-syntax-highlighting](https://github.com/zdharma-continuum/fast-syntax-highlighting)
		- [zsh-users/zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
		- [zsh-users/zsh-completions](https://github.com/zsh-users/zsh-completions)
- ✅️ [Hyper](https://hyper.is/) - 跨平台的终端软件
    - [awesome-hyper](https://github.com/bnb/awesome-hyper)
    - 配置文件位置：`~\AppData\Roaming\Hyper\.hyper.js`
    - `fontFamily: 'FiraCode Nerd Font, Input Mono, monospace'`

```bash
$ hyper install hyper-dracula
$ hyper install hyperborder
$ hyper install hyperpower
```

- ✅ [clink](https://chrisant996.github.io/clink/clink.html) - 为 CMD 提供丰富的补全、历史记录和行编辑功能
    - [popular-scripts](https://chrisant996.github.io/clink/clink.html#popular-scripts)

```bash
$ clink info
$ clink autorun install    # 启用自动运行
$ clink autorun uninstall  # 禁用自动运行
$ clink inject             # 临时运行

$ scoop hold clink         # 禁止更新
```

- ✅ [Starship](https://starship.rs/zh-CN/) - 轻量、迅速、客制化的高颜值终端

```bash
# powershell 7
Invoke-Expression (&starship init powershell)
$ENV:STARSHIP_CONFIG = "$HOME\\.config\\starship\\starship.toml"

# powershell 5
Invoke-Expression (& "$env:SCOOP\\apps\\starship\\current\\starship.exe" init powershell)
$ENV:STARSHIP_CONFIG = "$HOME\\.config\\starship\\starship.toml"

# cmd 在 clink\current\scripts 文件中添加 starship.lua
load(io.popen('starship init cmd'):read("*a"))()
os.setenv('STARSHIP_CONFIG', "$HOME\\.config\\starship\\starship.toml")
```

### 💻️ 开发环境

```bash
# 设置本地默认分支 main
$ git config --global init.defaultBranch main

# 设置文件大小写敏感
$ git config --global core.ignorecase false

# 忽略目录安全限制
$ git config --global --add safe.directory "*"

# 管理员身份运行 PowerShell
$ get-ExecutionPolicy
$ set-ExecutionPolicy RemoteSigned

$ $PROFILE                                    # powershell 配置文件地址
$ code $PROFILE                               # 直接打开配置文件
$ $psversiontable                             # powershell 版本
```

- ✅ [fnm](https://github.com/Schniz/fnm) - 快速简单的 Node 版本管理器

```bash
# fnm 支持多项目单独切换版本
$ echo 'eval "$(fnm env --use-on-cd)"' >> ~/.zshrc
$ source ~/.zshrc

# powershell 7 & powershell 5 需配置
# fnm
fnm env --use-on-cd | Out-String | Invoke-Expression
# fnm end

# cmd 在目标路径后追加
/k %USERPROFILE%\bashrc.cmd
# 在 ~ 目录下创建 bashrc.cmd，内容如下：
@echo off
FOR /f "tokens=*" %%z IN ('fnm env --use-on-cd') DO CALL %%z
# end

$ fnm ls
$ fnm ls-remote
$ fnm ls-remote | grep v20
$ fnm install --lts
$ fnm install --latest
$ fnm install 16.14.2
$ fnm install 14.16.0
$ fnm default X
$ fnm use X

# 项目写入 node 版本
$ node --version > .node-version
```

- ✅ 自定义 npm 全局包安装位置

```bash
$ npm config set prefix ~/.npm_global
```

```bash
# 全局安装 ni 及配置
$ npm i -g @antfu/ni

#  powershell 7
Remove-Alias -Name ni -Force
# end

# powershell 5
if (-not (Test-Path $profile)) {
  New-Item -ItemType File -Path (Split-Path $profile) -Force -Name (Split-Path $profile -Leaf)
}
Remove-Item Alias:ni -Force -ErrorAction Ignore
# end
```

### 💻️ 其它工具

- ✅ [微信键盘](https://z.weixin.qq.com/)
- ✅ [IDM](https://vip.jokerps.com/?s=idm&type=post) - 是一款优秀下载工具
- ✅ [Mihomo Party](https://github.com/mihomo-party-org/mihomo-party) - 更易用的代理客户端
- ✅ [SwitchHosts](https://switchhosts.vercel.app/zh) - 管理切换多个 hosts 的工具 | [GitHub Hosts](https://ineo6.github.io/hosts/)
- ✅ [LocalSend](https://localsend.org/) - 免费、开源、跨平台，将文件分享到附近的设备
- ✅ [FSCapture](https://www.faststone.org/) - 强大、轻便但功能齐全的屏幕捕捉和屏幕录像工具（网上随便搜索注册码）
- ✅ [PixPin](https://pixpinapp.com/) - 功能强大使用简单的截图/贴图工具
- ✅ [金山毒霸垃圾清理独立版](https://vip.jokerps.com/6164.html) - 短小精悍垃圾清理工具
- ✅ [PicGo](https://molunerfinn.com/PicGo/) - 图片上传 - 管理新体验
- ✅ [Watt Toolkit](https://steampp.net/) - 开源跨平台的多功能 Steam 工具箱
- ✅ [护眼宝](https://pc.qq.com/detail/7/detail_22407.html)

### ♻️ 资源平台

- ✅ [鹏少资源网](https://vip.jokerps.com/)
- ✅ [软件小妹](http://add.qianqian.club/)
