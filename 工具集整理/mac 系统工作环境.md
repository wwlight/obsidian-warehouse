#mac #安装 #命令

```ad-note
title: 说明
工欲善其事，必先利其器。
```

### ℹ️ 说明

- 省事方式：可借助 [Mac 迁移助理](https://support.apple.com/zh-cn/102613) 进行快速同步
- ✅：免费｜推荐
- ❎：收费｜了解｜科学

### 🍀 准备工作

- ✅ [Homebrew](https://brew.sh/) - 软件包的管理器｜[镜像](https://gitee.com/cunkai/HomebrewCN) `[!!success: 推荐]`
- ❎️ [Ghelper](https://ghelper.net/) - 浏览器插件 | [极简插件](https://chrome.zzzmh.cn/)
- ✅ [Mihomo Party](https://github.com/mihomo-party-org/mihomo-party) - 更易用的代理客户端
- ✅ [SwitchHosts](https://switchhosts.vercel.app/zh) - 管理切换多个 hosts 的工具 | [GitHub Hosts](https://ineo6.github.io/hosts/)
- ✅ [Nerd Fonts](https://www.nerdfonts.com/font-downloads) - 为开发者提供**图标字体**补丁

````ad-summary
title: 常用工具下载
collapse: false

```bash
$ brew install git
$ brew install starship
$ brew install fnm
$ brew install pnpm
$ brew install gh
$ brew install bun
$ brew install gping
$ brew install onefetch
$ brew install fzf
$ brew install zoxide
$ brew install tlrc  # 控制台命令速查表 tldr-pages
$ brew install git-extras  # git 增强扩展工具
$ brew install lsd
$ brew install lazygit
$ brew install nginx
$ brew install mysql
$ brew install code-server

$ brew install --cask arc
$ brew install --cask google-chrome
$ brew install --cask mihomo-party
$ brew install --cask visual-studio-code
$ brew install --cask cursor
$ brew install --cask webstorm
$ brew install --cask intellij-idea
$ brew install --cask hbuilderx
$ brew install --cask hyper
$ brew install --cask tabby
$ brew install --cask raycast
$ brew install --cask obsidian
$ brew install --cask ngrok
$ brew install --cask loop
$ brew install --cask cleanshot
$ brew install --cask screen-studio
$ brew install --cask switchhosts
$ brew install --cask keycastr
$ brew install --cask picgo

$ brew install syncthing
$ brew install --cask applite
$ brew install --cask browserosaurus
$ brew install --cask android-studio
$ brew install --cask android-platform-tools
$ brew install --cask vmware-fusion  # 免费虚拟机

$ brew install --cask font-fira-code-nerd-font
$ brew install --cask font-fira-mono-nerd-font
$ brew install --cask font-lxgw-wenkai
$ brew install --cask font-monaspace
$ brew install --cask font-maple-mono-nf-cn
$ brew install --cask font-symbols-only-nerd-font
```
````

### ✍🏻 终端配置

- ✅ [zsh](https://www.zsh.org/) - 功能强大的 shell
	- 系统自带
	- zsh plugins：
		- [zdharma-continuum/fast-syntax-highlighting](https://github.com/zdharma-continuum/fast-syntax-highlighting)
		- [zsh-users/zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
		- [zsh-users/zsh-completions](https://github.com/zsh-users/zsh-completions)
		- [incr](https://mimosa-pudica.net/zsh-incremental.html)
	- & 参考资料：[Using ZSH without OMZ](https://dev.to/hbenvenutti/using-zsh-without-omz-4gch)、[npm completion](https://didiaohu.gitbooks.io/npm/content/yong-npm-script-da-zao-chao-liu-de-qian-duan-gong-zuo-liu/23-shi-xian-ming-ling-xing-zi-dong-bu-quan.html)

```bash
$ touch $HOME/.zsh/plugins
$ touch $HISTFILE

$ git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git $HOME/.zsh/plugins/fast-syntax-highlighting
$ git clone https://github.com/zsh-users/zsh-autosuggestions.git $HOME/.zsh/plugins/zsh-autosuggestions
$ git clone https://github.com/zsh-users/zsh-completions.git $HOME/.zsh/plugins/zsh-completions
$ git clone https://github.com/marlonrichert/zsh-hist.git $HOME/.zsh/plugins/zsh-hist
```

- ✅️ [Hyper](https://hyper.is/) - 是一款跨平台的终端软件
	- [awesome-hyper](https://github.com/bnb/awesome-hyper)
	- 配置文件位置：`~/Library/Application Support/Hyper/.hyper.js`
    - `fontFamily: 'FiraCode Nerd Font, Input Mono, monospace'

```bash
$ hyper install hyper-dracula
$ hyper install hyperborder
$ hyper install hyperpower
```

- ✅ [Starship](https://starship.rs/zh-CN/) - 轻量、迅速、客制化的高颜值终端

```bash
$ cd .config && mkdir starship && cd starship && type null>starship.toml
```

### 💻️ 开发环境

```bash
# 设置本地默认分支 main
$ git config --global init.defaultBranch main

# 设置文件大小写敏感
$ git config --global core.ignorecase false

# 忽略目录安全限制
$ git config --global --add safe.directory "*"
```

- ✅ [fnm](https://github.com/Schniz/fnm) - 快速简单的 Node.js 版本管理器

```bash
# fnm 支持多项目单独切换版本
$ echo 'eval "$(fnm env --use-on-cd)"' >> ~/.zshrc
$ source ~/.zshrc

$ fnm ls
$ fnm ls-remote
$ fnm ls-remote | grep v20
$ fnm install --lts
$ fnm install --latest
$ fnm install 16.14.2
$ fnm install 14.16.0
$ fnm default X
$ fnm use X
$ fnm env

# 项目写入 node 版本
$ node --version > .node-version
```

```sh
$ pnpm setup
$ pnpm self-update
```

- ✅ 自定义 npm 全局包安装位置

```bash
$ mkdir -p ~/.npm_global
$ npm config set prefix ~/.npm_global

# 设置环境变量
echo "# 自定义 npm 全局包安装路径" >> ~/.zshrc
echo "export PATH=~/.npm_global/bin:$PATH" >> ~/.zshrc
echo "# end" >> ~/.zshrc
$ source ~/.zshrc

$ npm i -g @antfu/ni
```

### 💻️ 办公工具

- ✅ [Raycast](https://www.raycast.com/) - 一个为 mac 设计的高效生产力工具
- ️❎️ [Applite](https://aerolite.dev/applite/index.html) - 简化使用 Homebrew 的第三方应用程序的安装和管理
- ✅ [微信键盘](https://z.weixin.qq.com/)
- ✅ [Arc](https://arc.net/) - 浏览器
- ✅ [CleanMyMac X](https://cleanmymac.com/) - mac 清洁应用程序 | [国内代理商](https://www.mycleanmymac.com/triallp.html?utm_medium=wm&utm_source=wm.makeding.com&utm_content=buy_cmmx493_buy&utm_campaign=LM&utm_term=Janetwo&wm_cs_key=0db9266c-0b3f-4808-b176-99c97c3319fc)
- ✅ [Tabby](https://tabby.sh/) - 跨平台终端应用程序，本地 shell、串行、SSH 和 Telnet 连接
- ✅ [iShot Pro](https://apps.apple.com/cn/app/ishot-pro-%E4%B8%93%E4%B8%9A%E7%9A%84%E6%88%AA%E5%9B%BE%E8%B4%B4%E5%9B%BE%E5%BD%95%E5%B1%8F%E5%BD%95%E9%9F%B3ocr%E7%BF%BB%E8%AF%91%E5%8F%96%E8%89%B2%E5%B7%A5%E5%85%B7/id1611347086?mt=12) - 专业的截图贴图录屏录音 OCR 翻译取色工具
- ❎️ [CleanShot X](https://cleanshot.com/) - 功能强大的屏幕捕捉工具
- ❎️ [Screen Studio](https://screen.studio/) - 屏幕录制软件
- ✅ [右键助手专业版](https://apps.apple.com/cn/app/%E5%8F%B3%E9%94%AE%E5%8A%A9%E6%89%8B%E4%B8%93%E4%B8%9A%E7%89%88/id1555844307?mt=12) - 超丰富的右键菜单
- ✅ [Loop](https://github.com/MrKai77/Loop) - 简化窗口管理
- ✅ [Browserosaurus](https://browserosaurus.com/) - 适用于 mac 多浏览器用户
- ✅ [Kap](https://getkap.co/) - GIF 录制
- ✅ [The Unarchiver](https://theunarchiver.com/) - 解压工具
- ✅ [IINA](https://iina.io/) - 现代媒体播放器
- ✅ [Obsidian](https://obsidian.md/) - 是一款私密且灵活的写作应用程序
- ✅ [Command X](https://sindresorhus.com/command-x) - 在 Finder 中剪切和粘贴文件
- ✅ [KeyCastr](https://github.com/keycastr/keycastr) - 一个开源的按键可视化工具
- ❎ [Picture View](https://wl879.github.io/apps/picview/) - mac 图片浏览应用
- ✅ [PicGo](https://molunerfinn.com/PicGo/) - 图片上传 - 管理新体验
- ✅ [LocalSend](https://localsend.org/) - 免费、开源、跨平台，将文件分享到附近的设备
- ✅ [多邻国](https://apps.apple.com/cn/app/%E5%A4%9A%E9%82%BB%E5%9B%BDduolingo%E8%8B%B1%E8%AF%AD%E6%97%A5%E8%AF%AD%E6%B3%95%E8%AF%AD/id570060128) - 全球数亿语言学习者的口碑选择
- ✅ [万词王](https://apps.apple.com/cn/app/%E4%B8%87%E8%AF%8D%E7%8E%8B-%E8%A7%86%E9%A2%91%E8%83%8C%E5%8D%95%E8%AF%8D%E5%AD%A6%E8%8B%B1%E8%AF%AD%E5%BF%85%E5%A4%87app/id1464643633) - 视频背单词学英语必备 APP
- ✅ [微信读书](https://apps.apple.com/us/app/%E5%BE%AE%E4%BF%A1%E8%AF%BB%E4%B9%A6/id952059546)
- ✅ [新华字典](https://apps.apple.com/cn/app/%E6%96%B0%E5%8D%8E%E5%AD%97%E5%85%B8-%E6%96%B0%E4%B8%AD%E5%9B%BD%E9%A2%87%E5%85%B7%E5%BD%B1%E5%93%8D%E5%8A%9B%E7%9A%84%E7%8E%B0%E4%BB%A3%E6%B1%89%E8%AF%AD%E5%AD%97%E5%85%B8/id1197209563)
- ❎ [Scroll Reverser](https://pilotmoon.com/scrollreverser/) - 触摸板与鼠标滚动方向独立设置

### ♻️ 资源平台

- ✅ [macOSicons](https://macosicons.com/) - 更换 mac 应用图标
- ✅ [Dockhunt](https://www.dockhunt.com/) - 程序坞应用分享平台
- ✅ [麦软网](https://www.mairuan.com/) - 专业正版低价软件
- ✅ [数码荔枝](https://lizhi.shop/) - 专注于分享最新鲜优秀的正版软件
- ❎ [MacKed](https://macked.app/) - 专注于 mac 软件分享与下载
- ✅ [awesome-mac](https://github.com/jaywcjlove/awesome-mac)
- ✅ [AppStorrent](https://appstorrent.org/)
- ✅ [XMac](https://xmac.app/)
- ✅ [XClient](https://xclient.info/)
- ✅ [Digit77](https://www.digit77.com/)
- ✅ [MacWK](https://macwk.cn/)
- ✅ [MacBL](https://www.macbl.com/)
- ❎ [MacApp分享频道](https://macapp.org.cn/)
- ✅ [IDEA 破解](https://o1h17wcfnl0.feishu.cn/docx/KwacdbYSkoOn1exdopVcADU0noa)
- ✅ [适用于苹果芯片了吗？](https://isapplesiliconready.com/zh) - 应用程序指南
