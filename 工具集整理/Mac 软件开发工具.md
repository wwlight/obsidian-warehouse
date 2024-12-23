### [Homebrew](https://brew.sh/) 包管理工具

>[!note] 说明
>简称 brew，是 macOS 和 Linux 上最流行的包管理工具，它可以帮助你安装、更新和管理软件包。类似于 Ubuntu 的 apt 或 CentOS 的 yum。

##### 安装
```sh
# 官网安装地址
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# M 系列芯片国内镜像
$ /bin/zsh -c "$(curl -fsSL https://gitee.com/huwei1024/HomebrewCN/raw/master/Homebrew.sh)"

# inter 芯片国内镜像
$ /bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

##### 常用命令
```sh
$ brew config                         # 显示配置信息
$ brew update                         # 更新软件包列表
$ brew update-reset                   # 强制更新到最新版本，update 失败可尝试

$ brew doctor                         # 检查系统是否有问题
$ brew autoremove                     # 删除没有被其他包依赖的依赖包
$ brew cleanup                        # 清理相关的旧版本和缓存文件

$ brew search [软件名]                 # 搜索软件包
$ brew list/ls                        # 列出所有已安装的软件
$ brew info [软件名]                   # 显示软件包信息
$ brew home [软件名]                   # 打开软件包主页
$ brew install [软件名]                # 安装软件
$ brew uninstall [软件名]              # 卸载软件
$ brew install --cask [应用名]         # 安装 GUI 应用程序
$ brew upgrade                        # 更新所有安装的包
$ brew upgrade [软件名]                # 更新指定安装包

$ brew services list/ls               # 查看所有服务状态
$ brew services start [服务名]         # 启动服务
$ brew services stop [服务名]          # 停止服务
$ brew services restart [服务名]       # 重启服务

$ brew deps [软件名]                   # 查看包的依赖关系
$ brew outdated                       # 列出可以升级的软件
$ brew uses [软件名] --installed       # 查看哪些包依赖于这个包 
```

##### 常用安装应用
```sh
$ brew install git
$ brew install starship
$ brew install gh
$ brew install bun
$ brew install nginx
$ brew install mysql
$ brew install code-server
$ brew install gping
$ brew install onefetch
$ brew install fzf
$ brew install zoxide
$ brew install lazygit

$ brew install --cask applite
$ brew install --cask visual-studio-code
$ brew install --cask cursor
$ brew install --cask webstorm
$ brew install --cask intellij-idea
$ brew install --cask hbuilderx
$ brew install --cask hyper
$ brew install --cask warp
$ brew install --cask raycast
$ brew install --cask obsidian
$ brew install --cask loop
$ brew install --cask cleanshot
$ brew install --cask screen-studio
$ brew install --cask switchhosts
$ brew install --cask keycastr
$ brew install --cask browserosaurus
$ brew install --cask android-studio
$ brew install --cask android-platform-tools
$ brew install --cask picgo
```
##### 部分工具使用配置
###### adb wifi 手机调试
- <font color="#00b050">初始先用数据线将手机和电脑连接</font>
```sh
# mac
$ adb tcpip 5555

# 查看手机 ip
# mac/window
$ adb shell ifconfig wlan0

# 连接手机
$ adb connect 192.168.xx.xxx

# 断开连接
$ adb disconnect 192.168.xx.xxx

# 其他
$ adb kill-server
```
###### code-server 常用命令
```sh
$ brew install code-server
$ brew uninstall code-server
$ brew info code-server              # 显示 code-server 信息
$ brew services start code-server
$ brew services stop code-server
$ brew services restart code-server
$ code-server
$ code-server start
$ code-server restart
$ code-server info                   # 查看基本信息

# code-server 同步本地 VSCode 配置
$ ln -s ~/.vscode/extensions ~/.local/share/code-server

$ ln -s ~/.config/Code/User ~/.local/share/code-server
# 若没有 ~/.config/Code/User 文件，执行
$ ln -s ~/Library/Application\ Support/Code/User ~/.local/share/code-server 

$ ln -s ~/.config/Code/Backups ~/.local/share/code-server
# 若没有 ~/.config/Code/Backups 文件，执行
$ ln -s ~/Library/Application\ Support/Code/Backups ~/.local/share/code-server 
```
###### Nginx 常用命令
```sh
$ brew install nginx
$ brew uninstall nginx
$ brew info nginx                    # 显示 nginx 信息
$ brew services start nginx          # 启动 nginx 服务
$ brew services stop nginx           # 停止 nginx 服务
$ brew services restart nginx        # 重启 nginx 服务（修改配置）
$ nginx -t                           # 检查配置文件是否正确
$ nginx -s reload                    # 重新加载配置文件（修改配置文件后，无需重启）
$ nginx                              # 运行 nginx（非服务模式，临时运行）
$ nginx -s stop                      # 停止临时运行的 nginx
$ nginx -s quit                      # 安全关闭临时运行的 nginx
$ nginx -s reopen                    # 打开日志文件
$ nginx -v                           # 查看 nginx 的版本
$ nginx -V                           # 查看完整的 nginx 编译参数

$ ps aux | grep nginx                # 确认启动用户
$ sudo kill -QUIT <process_pid>      # 关闭指定 Nginx 进程
$ sudo pkill -f nginx                # 关闭所有 Nginx 进程
```
###### MySQL 常用命令
```sh
$ brew install mysql
$ brew uninstall mysql
$ brew info mysql                    # 显示 MySQL 信息
$ brew services start mysql          # 启动 MySQL 服务
$ brew services stop mysql           # 停止 MySQL 服务
$ brew services restart mysql        # 重启 MySQL 服务
$ mysql.server start                 # 临时启动 MySQL
$ mysql.server stop                  # 停止临时运行的 MySQL
$ mysql -u root                      # 以默认用户登录 MySQL
$ mysql -u root -p                   # 以默认用户密码登录 MySQL
$ mysql_secure_installation          # 初次安装后设置 root 用户的密码
$ mysql --version                    # 查看 MySQL 版本
```
##### 常见问题
```sh
# brew services list 报错可尝试
$ brew untap homebrew/services        # 删除当前的 services
$ brew tap homebrew/services          # 重新安装
```

```sh
# brew services start nginx 出现警告
Warning: nginx must be run as non-root to start at user login!
Bootstrap failed: 5: Input/output error
Error: Failure while executing; `/bin/launchctl bootstrap system /Library/LaunchDaemons/homebrew.mxcl.nginx.plist` exited with 5.

# 解决方案：
$ brew services stop nginx
$ sudo rm -f ~/Library/LaunchAgents/homebrew.mxcl.nginx.plist
$ brew services start nginx

# 验证 `/opt/homebrew/` 的相关权限
$ sudo chown -R $(whoami):admin /opt/homebrew
```
###  [SDKMAN](https://sdkman.io/) 开发工具包管理工具

>[!info] 说明
>用来管理多个软件开发工具包（SDK）版本的工具，主要用于 Unix 系统（Mac、Linux），它的主要作用包括：
>1. 多版本管理
	>- 可以在同一系统上安装和管理多个版本的 Java、Kotlin、Groovy 等
	>- 方便地在不同版本间切换，比如项目A需要 Java 8，项目B需要 Java 17
>2. 简化安装过程
	>- 不需要手动下载、解压、配置环境变量
	>- 一行命令就能完成安装：`sdk install java 17.0.2-tem`
	>- 自动处理环境变量配置
>3. 支持多种开发工具
	>- Java (各种发行版如 OpenJDK, Oracle JDK, GraalVM)
	>- 构建工具（Maven, Gradle）
	>- 各种 JVM 语言（Kotlin, Groovy, Scala）
	>- Spring Boot, Micronaut 等框架
>4. 项目级版本管理
	>- 可以为不同项目设置不同的SDK版本
	>- 通过 .sdkmanrc 文件管理项目依赖的版本
>5. 版本更新
	>- 及时获取各种工具的最新版本
	>- 方便地进行版本升级和回退
>6. 实际使用场景：
	>- 开发者需要在不同 Java 版本间切换时
	>- 测试应用在不同 JDK 版本上的兼容性
	>- 团队统一开发环境配置
	>- 快速配置新的开发环境
##### 通过 [brew](https://github.com/sdkman/homebrew-tap) 安装
```sh
# install
$ brew tap sdkman/tap             # 允许 Homebrew 添加更多的软件源（额外的软件仓库）
$ brew install sdkman-cli

# .zshrc config
echo '# SDKMAN' >> ~/.zshrc
echo 'export SDKMAN_DIR=$(brew --prefix sdkman-cli)/libexec' >> ~/.zshrc
echo '[[ -s "${SDKMAN_DIR}/bin/sdkman-init.sh" ]] && source "${SDKMAN_DIR}/bin/sdkman-init.sh"' >> ~/.zshrc
echo '# SDKMAN end' >> ~/.zshrc
$ source ~/.zshrc

# uninstall
$ brew uninstall sdkman-cli
$ brew untap sdkman/tap
```
##### SDK 常用命令
```sh
$ sdk version                     # 查看版本
$ sdk help                        # 显示帮助信息
$ sdk list                        # 查看可安装的所有工具和版本
$ sdk current                     # 查看当前激活的工具及其版本
$ sdk env init                    # 初始化项目特定环境
$ sdk env install                 # 安装 .sdkmanrc 中定义的版本
$ sdk env                         # 显示当前环境信息
$ sdk update                      # 更新 SDKMAN
$ sdk upgrade                     # 列出可更新的软件版本
$ sdk upgrade java                # 更新特定软件到最新版
$ sdk flush                       # 清除缓存
$ sdk offline enable              # 启用离线模式
$ sdk offline disable             # 禁用离线模式
```
##### Java 安装
```sh
# 查看可用 java 版本，本地安装信息
$ sdk list java

# 安装 java 指定版本 
$ sdk install java 8.0.432-zulu
$ sdk install java 17.0.13-zulu 

# 设置默认版本
$ sdk default java 8.0.432-zulu

# 临时使用指定版本
$ sdk use java 8.0.432-zulu

# 查看指定版本安装路径
$ sdk home java 8.0.432-zulu

# 查看 java 版本
$ java -version
$ javac -version
```
##### Maven 安装
```sh
# 列出特定软件可用版本
$ sdk list maven									

# 安装最新稳定版
$ sdk install maven		
# 安装指定版本
$ sdk install maven 3.9.8					

# 设置默认版本
$ sdk default maven 3.9.9

# 临时使用指定版本
$ sdk use maven 3.9.9

# 查看指定版本安装路径
$ sdk home maven 3.9.9

# 查看 maven 版本
$ mvn -v
```