#windows #安装 #命令

```ad-info
title: 说明
工欲善其事，必先利其器。
```

### ℹ️ 说明

- ✅：免费｜推荐
- ❎：收费｜了解｜科学

### 🍀 准备工作

- 🗂️ 创建文件夹：`DevelopmentApplication`、`SystemApplication`

```bash
$ md D:\DevelopmentApplication
$ md D:\SystemApplication
```

- ❎️ [Ghelper](https://ghelper.net/) - 浏览器插件 | [极简插件](https://chrome.zzzmh.cn/)
- ✅ [Mihomo Party](https://github.com/mihomo-party-org/mihomo-party) - 更易用的代理客户端
- ✅ [SwitchHosts](https://switchhosts.vercel.app/zh) - 管理切换多个 hosts 的工具 | [GitHub Hosts](https://ineo6.github.io/hosts/)
- ✅ [Nerd Fonts](https://www.nerdfonts.com/font-downloads) - 为开发者提供**图标字体**补丁
- ✅ [Scoop](https://scoop.sh/) - 适用于 Windows 的命令行安装程序 | [镜像](https://gitee.com/scoop-installer/scoop)

```bash
# 第一步：设置安装目录
$ $env:SCOOP='D:\DevelopmentApplication\Scoop'
$ [Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')

# 第二步：开启代理，在 powershell 中安装
$ Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
$ iex "& {$(irm get.scoop.sh)} -RunAsAdmin"

$ scoop import scoop_backup.json
```

![[scoop_backup.json]]

````ad-summary
title: Scoop 常用命令
collapse: closed

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
````

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
$ scoop install fnm
$ scoop install pnpm
$ scoop install gsudo
$ scoop install gping
$ scoop install fzf
$ scoop install zoxide
$ scoop install nginx
$ scoop install ngrok          # 反向代理，内网穿透
$ scoop install tlrc           # 控制台命令速查表 tldr-pages
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
$ scoop install gh
$ scoop install tabby          # 本地 shell、串行、SSH 和 Telnet 连接终端
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

### ✍🏻 终端配置

- ✅ [zsh](https://www.zsh.org/) - 功能强大的 shell
	- 将 [zsh 安装包](https://packages.msys2.org/packages/zsh?repo=msys&variant=x86_64) 解压到 git 的安装根目录下
	- Zsh plugins：
		- [zdharma-continuum/fast-syntax-highlighting](https://github.com/zdharma-continuum/fast-syntax-highlighting)
		- [zsh-users/zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
		- [zsh-users/zsh-completions](https://github.com/zsh-users/zsh-completions)
	- & 参考资料：[Using ZSH without OMZ](https://dev.to/hbenvenutti/using-zsh-without-omz-4gch)、[npm completion](https://didiaohu.gitbooks.io/npm/content/yong-npm-script-da-zao-chao-liu-de-qian-duan-gong-zuo-liu/23-shi-xian-ming-ling-xing-zi-dong-bu-quan.html)

```bash
$ md $HOME/.zsh/plugins
$ touch $HISTFILE # 安装成功才能使用

$ git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git $HOME\.zsh\plugins\fast-syntax-highlighting
$ git clone https://github.com/zsh-users/zsh-autosuggestions.git $HOME\.zsh\plugins\zsh-autosuggestions
$ git clone https://github.com/zsh-users/zsh-completions.git $HOME\.zsh\plugins\zsh-completions
```

````ad-info
title: .bashrc 配置文件
collapse: closed

```bash
if [ -t 1 ]; then
	exec zsh
fi
```
````

````ad-info
title: .zshrc 配置文件
collapse: closed

```bash
# ~/.zshrc
export ZSH=$HOME/.zsh
export ZSH_COMPDUMP=$ZSH/cache/.zcompdump-$HOST
export HISTFILE=$ZSH/.zsh_history
export HISTSIZE=5000
export SAVEHIST=5000
setopt appendhistory
setopt incappendhistory        # 实时写入，避免丢失
unsetopt sharehistory          # 禁用共享，防止竞争
setopt extended_history        # 记录时间戳
setopt hist_ignore_all_dups    # 完全去重
setopt hist_save_no_dups       # 文件去重
setopt hist_find_no_dups       # 搜索去重
setopt hist_expire_dups_first  # 优先删除重复项
setopt hist_ignore_space       # 忽略以空格开头的命令
setopt hist_reduce_blanks      # 去除多余空格
setopt hist_ignore_dups        # 忽略连续重复命令
setopt hist_verify             # 执行历史命令前先显示
# zsh plugins
source $ZSH/plugins/fast-syntax-highlighting/fast-syntax-highlighting.plugin.zsh
source $ZSH/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
fpath=($ZSH/plugins/zsh-completions/src $fpath)
ZSH_AUTOSUGGEST_STRATEGY=(history completion)
ZSH_AUTOSUGGEST_BUFFER_MAX_SIZE=20
# plugins end

# fnm
eval "$(fnm env --use-on-cd)"
# fnm end

# fzf
source <(fzf --zsh)
# fzf end

# zoxide
eval "$(zoxide init zsh --cmd cd)"
function cdl() {
    local dir
    dir="$(zoxide query -l | fzf --reverse --height 40% \
        --preview 'ls -l {}' \
        --preview-window=right:60%)" && cd "${dir}"
}
function cdd() {
    local dir
    dir="$(find . -type d 2>/dev/null | fzf --reverse --height 40% \
        --preview 'ls -l {}' \
        --preview-window=right:60%)" && cd "${dir}"
}
# zoxide end

# starship
eval "$(starship init zsh)"
export STARSHIP_CONFIG=$HOME/.config/starship/starship.toml
function set_win_title(){
    echo -ne "\033]0; $(basename "$USER") \007"
}
starship_precmd_user_func="set_win_title"
precmd_functions+=(set_win_title)
# starship end

# uv python 版本管理工具
autoload -Uz compinit && compinit
eval "$(uv generate-shell-completion zsh)"
eval "$(uvx --generate-shell-completion zsh)"
# uv end

# alias
alias ping="gping"
alias of="onefetch"
alias nio="ni --prefer-offline"
alias s="nr start"
alias d="nr dev"
alias b="nr build"
alias cls="clear"
alias gp='git push'
alias gl='git pull'
alias grt='cd "$(git rev-parse --show-toplevel)"'
alias gc='git branch | fzf | xargs git checkout' # 搜索 git 分支并切换
alias t='tldr' # tldr
# alias end

# 添加清理历史记录的函数
function history_clean() {
    # 创建临时文件
    local tmp=$(mktemp)

    # Windows 上没有 tail -r，使用 awk 逆序读取
    awk '
    {
        # 保存所有行
        lines[NR] = $0;
    }
    END {
        # 反向处理每一行
        for (i = NR; i >= 1; i--) {
            line = lines[i];
            if (index(line, ";") > 0) {
                # 命令部分是分号后面的内容
                cmd = substr(line, index(line, ";") + 1);
                if (!seen[cmd]++) {
                    # 第一次遇到这个命令（因为是反向处理的，所以是最新的）
                    result[++count] = line;
                }
            } else {
                # 处理没有分号的行（可能是没有时间戳的记录）
                if (!seen[line]++) {
                    result[++count] = line;
                }
            }
        }

        # 恢复原来的顺序（再次反转）
        for (i = count; i > 0; i--) {
            print result[i];
        }
    }' $HISTFILE > $tmp

    # 确保处理成功后再替换原文件
    if [ -s "$tmp" ]; then
        cp $HISTFILE "$HISTFILE.bak"  # 创建备份
        mv $tmp $HISTFILE
        echo "历史记录已去重，保留了最新的命令记录"
    else
        echo "处理出错，历史记录未修改"
        rm $tmp
    fi
}
```
````

````ad-info
title: git-extras 安装
collapse: closed

```bash
$ git clone https://github.com/tj/git-extras.git
$ cd git-extras
$ git checkout $(git describe --tags $(git rev-list --tags --max-count=1))
$ ./install.cmd 'D:\DevelopmentApplication\Scoop\apps\git\current'
$ git extras --help
```
````

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

# 下载插件
$ git clone https://github.com/vladimir-kotikov/clink-completions D:\\DevelopmentApplication\\Scoop\\apps\\clink\\current\\scripts\\clink-completions
$ git clone https://github.com/chrisant996/clink-gizmos D:\\DevelopmentApplication\\Scoop\\apps\\clink\\current\\scripts\\clink-gizmos

$ clink installscripts D:\\DevelopmentApplication\\Scoop\\apps\\clink\\current\\scripts
$ clink installscripts D:\\DevelopmentApplication\\Scoop\\apps\\clink\\current\\scripts\\clink-completions
$ clink installscripts D:\\DevelopmentApplication\\Scoop\\apps\\clink\\current\\scripts\\clink-gizmos

# 使用方法
$ clink autorun install    # 启用自动运行
$ clink autorun uninstall  # 禁用自动运行
$ clink inject             # 临时运行

$ scoop hold clink         # 禁止更新
```

- ✅ [Starship](https://starship.rs/zh-CN/) - 轻量、迅速、客制化的高颜值终端

```bash
$ cd .config && mkdir starship && cd starship && type null>starship.toml

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

````ad-info
title: starship.toml 配置文件
collapse: closed

```bash
command_timeout = 10000

# 在提示符之间插入空行
add_newline = true

# 将提示符中的 '❯' 替换为 '➜'
[character] 
success_symbol = '[➜](bold green)'

# 禁用 'package' 组件，将其隐藏
[package]
disabled = true

[localip]
ssh_only = false
format = '[$localipv4](bold green) '
disabled = true

[cmd_duration]
min_time = 500
format = 'underwent [$duration](bold yellow)'
disabled = true
```
````

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
$ mkdir .npm_global
$ npm config set prefix ~/.npm_global

# 设置系统环境变量
C:\Users\wwlight\.npm_global
```

```bash
$ npm i -g nrm        # npm 镜像管理器
$ npm i -g pnpm
$ npm i -g yarn
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
