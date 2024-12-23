>[!info]
>工欲善其事，必先利其器。
###  ℹ️ 说明
+ ✅：免费｜推荐
+ ❎：收费｜了解｜科学
### 🍀 准备工作
+ 🗂️ 创建文件夹：`DevelopmentApplication`、`SystemApplication`
+ ✅ ️[Google Chrome](https://pc.qq.com/detail/1/detail_2661.html)【[官网](https://www.google.com/intl/zh-CN/chrome/)】- 一切事情的开始
    - 登录账号同步数据
+ ❎️ [Ghelper](https://ghelper.net/) - 【付费】浏览器插件，安全科学上网的第一步
    - 登录账号开通会员，开启新世界的大门
+ ✅ 字体安装
    - [Nerd Fonts](https://www.nerdfonts.com/font-downloads) - 修补了具有大量字形（图标）的开发人员目标字体
    - 搜索下载 `FiraCode Nerd Font`
+ ✅ [Scoop](https://scoop.sh/) - 适用于 Windows 的命令行安装程序 | [镜像](https://gitee.com/scoop-installer/scoop)
```bash
# 第一步：设置安装目录
$ $env:SCOOP='D:\DevelopmentApplication\Scoop'
$ [Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')

# 第二步：开启代理，在 powershell 中安装
$ Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
$ iex "& {$(irm get.scoop.sh)} -RunAsAdmin"

# 其它
$ scopp uninstall scoop
```
+ ✅ [SwitchHosts](https://switchhosts.vercel.app/zh) - 是一个管理、切换多个 hosts 方案的工具
    - [GitHub Hosts](https://ineo6.github.io/hosts/) - GitHub 最新 hosts
### ✍🏻 终端配置
+ ✅️ [Hyper](https://hyper.is/) - 是一款跨平台的终端软件
    - [awesome-hyper](https://github.com/bnb/awesome-hyper)
    - 配置文件位置：`~\AppData\Roaming\Hyper\.hyper.js`
```bash
$ hyper install hyper-dracula
$ hyper install hyperborder
$ hyper install hyperpower
```
+ ✅ [clink](https://chrisant996.github.io/clink/clink.html) - 为 CMD 提供丰富的补全、历史记录和行编辑功能
    - [popular-scripts](https://chrisant996.github.io/clink/clink.html#popular-scripts)
```bash
$ scoop install clink
$ clink info

# 下载插件
$ git clone https://github.com/vladimir-kotikov/clink-completions D:\DevelopmentApplication\Scoop\apps\clink\current\scripts\clink-completions
$ git clone https://github.com/chrisant996/clink-gizmos D:\DevelopmentApplication\Scoop\apps\clink\current\scripts\clink-gizmos

$ clink installscripts D:\DevelopmentApplication\Scoop\apps\clink\current\scripts
$ clink installscripts D:\DevelopmentApplication\Scoop\apps\clink\current\scripts\clink-completions
$ clink installscripts D:\DevelopmentApplication\Scoop\apps\clink\current\scripts\clink-gizmos
```
+ ✅ [Starship](https://starship.rs/zh-CN/) - 轻量、迅速、客制化的高颜值终端
```bash
$ scoop install starship
$ cd .config && mkdir starship && cd starship && type nul>starship.toml

# powershell 7
Invoke-Expression (&starship init powershell)
$ENV:STARSHIP_CONFIG = "$HOME\\.config\\starship\\starship.toml"
# end

# powershell 5
Invoke-Expression (& 'D:\DevelopmentApplication\Scoop\apps\starship\current\starship.exe' init powershell)
$ENV:STARSHIP_CONFIG = "$HOME\\.config\\starship\\starship.toml"
# end

# cmd 在 clink\current\scripts 文件中添加 starship.lua
load(io.popen('starship init cmd'):read("*a"))()
os.setenv('STARSHIP_CONFIG', 'C:\\Users\\<username>\\.config\\starship\\starship.toml')
# end
```
+ zsh plugins：
    - [zdharma-continuum/fast-syntax-highlighting](https://github.com/zdharma-continuum/fast-syntax-highlighting)
    - [zsh-users/zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
    - [zsh-users/zsh-completions](https://github.com/zsh-users/zsh-completions)

+ zsh settings：
>[!fap]- .zshrc 配置文件
>```
>export ZSH=$HOME/.zsh
>export ZSH_COMPDUMP=$ZSH/cache/.zcompdump-$HOST
>HISTFILE=$HOME/.zsh_history
>HISTSIZE=5000
>SAVEHIST=5000
>HISTDUP=erase
>setopt appendhistory
>setopt sharehistory
>setopt incappendhistory
>setopt hist_ignore_all_dups
>setopt hist_save_no_dups
>setopt hist_ignore_dups
>setopt hist_find_no_dups
>
># zsh plugins 
>source $ZSH/plugins/fast-syntax-highlighting/fast-syntax-highlighting.plugin.zsh
>source $ZSH/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
>fpath=($ZSH/plugins/zsh-completions/src $fpath)
>ZSH_AUTOSUGGEST_STRATEGY=(history completion)
>ZSH_AUTOSUGGEST_BUFFER_MAX_SIZE=20
># plugins end
>
>alias ping="gping"
>alias of="onefetch"
>alias nio="ni --prefer-offline"
>alias s="nr start"
>alias d="nr dev"
>alias b="nr build"
>alias z="zoxide"
>alias cls="clear"
># Go to project root
>alias grt='cd "$(git rev-parse --show-toplevel)"'
>alias gp='git push'
>alias gl='git pull'
>
># fnm
>eval "$(fnm env --use-on-cd)"
># fnm end
>
># starship
>eval "$(starship init zsh)"
>export STARSHIP_CONFIG=$HOME/.config/starship/starship.toml
>function set_win_title(){
 >   echo -ne "\033]0; $(basename "$USER") \007"
>}
>starship_precmd_user_func="set_win_title"
>precmd_functions+=(set_win_title)
># starship end
>
># zoxide
>eval "$(zoxide init zsh)"
># zoxide end
>
># fzf
>source <(fzf --zsh)
># fzf end
>```
+ 参考资料：[Using ZSH without OMZ](https://dev.to/hbenvenutti/using-zsh-without-omz-4gch)、[npm completion](https://didiaohu.gitbooks.io/npm/content/yong-npm-script-da-zao-chao-liu-de-qian-duan-gong-zuo-liu/23-shi-xian-ming-ling-xing-zi-dong-bu-quan.html)
### 💻️ 开发工具
```bash
$ scoop install git
$ scoop install gh
$ scoop install pnpm
$ scoop install yarn
$ scoop install bun
$ scoop install gsudo
$ scoop install gping
$ scoop install onefetch
$ scoop install adb
$ scoop install fzf
$ scoop install zoxide

$ scoop install extras/hyper
$ scoop install extras/switchhosts
```
+ ✅ [VS Code](https://code.visualstudio.com/) - 登录账号同步数据
+ ✅ [Hbuilder X](https://www.dcloud.io/hbuilderx.html)
+ ✅ [electerm](https://electerm.html5beta.com/)
+ ✅ [GitHub Cli](https://cli.github.com/)
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

# powershell 配置文件
$ $PROFILE

# powershell 版本
$ $psversiontable
```
+ ✅ [fnm](https://github.com/Schniz/fnm) - 快速简单的 Node.js 版本管理器，用 Rust 构建
```bash
# fnm 支持多项目单独切换版本
$ scoop install fnm
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
+ ✅ [Corepack](https://github.com/nodejs/corepack) - 允许您使用 Yarn、npm 和 pnpm，默认随 node 一起安装 （ v16.9.0+）
```bash
$ corepack -h
$ corepack enable

$ corepack install -g pnpm
$ corepack install -g yarn

# 切换 pnpm 最新版本
$ corepack use pnpm@latest
# 切换 pnpm 指定版本
$ corepack use pnpm@9.0.6  
```
+ 共享 npm 全局模块
```bash
$ mkdir .npm_global
$ npm config set prefix ~/.npm_global
# 设置系统环境变量
C:\Users\wwlight\.npm_global

# 全局安装 ni 及配置
$ npm i -g @antfu/ni
#  powershell 7
Remove-Alias -Name ni -Force
# end
#  powershell 5
if (-not (Test-Path $profile)) {
  New-Item -ItemType File -Path (Split-Path $profile) -Force -Name (Split-Path $profile -Leaf)
}
Remove-Item Alias:ni -Force -ErrorAction Ignore
# end
```
### 💻️ 系统工具
+ ✅[ 微信键盘](https://z.weixin.qq.com/)
+ ✅ [Clash for Windows](https://clashforwindows.org/)
+ ✅ [Quicker](https://getquicker.net/)
+ ✅ [flowlauncher](https://www.flowlauncher.com/) - Quick File Search & App Launcher for Windows
+ ✅ [IDM](https://vip.jokerps.com/?s=idm&type=post) - 是一款优秀下载工具
+ ✅ [Potplayer](https://potplayer.daum.net/) - 万能播放器
+ ✅ [FSCapture](https://www.faststone.org/) - 强大、轻便但功能齐全的屏幕捕捉 和 屏幕录像 工具（网上随便搜索注册码）
+ ✅ [PixPin](https://pixpinapp.com/) - 功能强大使用简单的截图/贴图工具
+ ✅ [金山毒霸垃圾清理独立版](https://vip.jokerps.com/6164.html) - 短小精悍垃圾清理工具
+ ✅ [WinRAR](https://www.winrar.com.cn/) - 是一款功能强大的压缩包管理器
+ ✅ [Obsidian](https://obsidian.md/) - 是一款私密且灵活的写作应用程序
+ ✅ [PicGo](https://molunerfinn.com/PicGo/) - 图片上传+管理新体验
+ ✅ [Keyviz](https://mularahul.github.io/keyviz/) - 一个免费开源按键可视化工具
+ ✅ [护眼宝](https://pc.qq.com/detail/7/detail_22407.html)

### ♻️ 资源平台
+ ✅ [鹏少资源网](https://vip.jokerps.com/)