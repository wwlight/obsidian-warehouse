###  [SDKMAN](https://sdkman.io/) 
>[!info] 说明
>用来管理多个软件开发工具包(SDK)版本的工具，主要用于 Unix 系统（Mac、Linux），它的主要作用包括：
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
##### [ brew 安装](https://github.com/sdkman/homebrew-tap)
```sh
# install
$ brew tap sdkman/tap        	# 允许 Homebrew 添加更多的软件源（额外的软件仓库）
$ brew install sdkman-cli

# .zshrc config
$ echo '# SDKMAN\nexport SDKMAN_DIR=$(brew --prefix sdkman-cli)/libexec\n[[ -s "${SDKMAN_DIR}/bin/sdkman-init.sh" ]] && source "${SDKMAN_DIR}/bin/sdkman-init.sh"\n# SDKMAN end' >> ~/.zshrc
$ source ~/.zshrc

# uninstall
$ brew uninstall sdkman-cli
$ brew untap sdkman/tap
```
##### SDK 常用命令
```sh
$ sdk version				# 查看版本
$ sdk help					# 显示帮助信息
$ sdk list					# 查看可安装的所有工具和版本
$ sdk current				# 查看当前激活的工具及其版本
$ sdk env init				# 初始化项目特定环境
$ sdk env install			# 安装 .sdkmanrc 中定义的版本
$ sdk env					# 显示当前环境信息
$ sdk update               	# 更新 SDKMAN
$ sdk upgrade             	# 列出可更新的软件版本
$ sdk upgrade java        	# 更新特定软件到最新版
$ sdk flush               	# 清除缓存
$ sdk offline enable      	# 启用离线模式
$ sdk offline disable     	# 禁用离线模式
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