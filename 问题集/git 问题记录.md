### Git 仓库中文件或目录的大小写敏感

- ! Git 默认情况下对文件名大小写不敏感
- 第一步：首先确保本地 Git 配置启用大小写敏感

```sh
$ git config --global core.ignorecase false
$ git config --local core.ignorecase false

# 查询状态
$ git config --get core.ignorecase
$ git config --local --get core.ignorecase
```

- 第二步：使用 git mv 命令进行重命名 (假设要将 demo 改为 Demo)

```sh
# 先改成临时名称
$ git mv filename demo.tmp
# 再改成目标名称
$ git mv demo.tmp Filename
``` 

- 针对文件已经提交过（线上大小写同时存在），需要清除缓存再提交

``` sh
# 移除要删除的文件缓存
$ git rm --cached filename
```

### Git 强制同步远程最新代码

- 代码回滚导致本地与远程版本不一致，无法直接拉取远程仓库

```bash
# 检出远程所有分支最新数据
$ git fetch --all
$ git reset --hard origin/main # 丢弃本地
```

### 重新关联本地项目到远程 Git 仓库

- 场景：误删除了本地 Git 项目的 `.git` 目录

```sh
$ git init
$ git remote add origin <origin_url>
$ git fetch
$ git reset --hard origin/main # 丢弃本地
$ git branch --set-upstream-to=origin/main main # 设置上游跟踪
# 等价于
$ git checkout -B main origin/main
``` 

### Git LFS 大文件存储

```ad-info
title: 说明

- 用于对大文件进行版本控制的开源 Git 扩展
- [Git Large File storage](https://git-lfs.com/)
- [GitHub 管理大型文件](https://docs.github.com/zh/repositories/working-with-files/managing-large-files/about-large-files-on-github)
```

##### Git LFS 原理

- Git LFS 通过懒惰地 (lazily) 下载大文件的相关版本来减少大文件在仓库中的影响。具体来说, 大文件是在 `checkout` 的过程中下载的, 而不是 `clone` 或 `fetch` 过程中下载的。
- Git LFS 通过将仓库中的大文件替换为小于 1 KB 的指针文件来做到这一点。在正常使用期间, 我们不会看到这些指针文件, 因为它们是由 Git LFS 自动处理的:
	- 当我们执行 `git add` 命令时, Git LFS 用一个指针替换实际内容,  
		并将实际内容存储在本地 LFS 缓存中 (本地缓存位于仓库的 _.git/lfs/objects_ 路径下）。
	- `git push` 时新增的 commit 所引用的所有 `大文件` 都会从本地传输到远程仓库的远程存储。
	- 当我们 `checkout` 一个包含 Git LFS 指针的 commit 时 (`pull` 包含了 `checkout` 命令),  
		指针文件将替换为本地 Git LFS 缓存中的文件, 或者从远端 Git LFS 存储区下载。
![[git-lfs-graphic.gif]]

##### Git LFS 好处

- 对于日常使用 Git 的习惯不造成影响。
- 减小本地 Git 缓存所占用的存储空间。
- 加快 `git fetch` 或 `git pull` 的速度。
- 加快在 commit 之间切换的速度。

##### Git LFS 使用方式

```sh
# windows 安装 
$ scoop install git-lfs
# mac 安装
$ brew install git-lfs

# 检查
$ git lfs --version

# 初始化工程，开启
$ git lfs install
$ git lfs install --local

# 将 .png 文件格式设置为被 Git LFS 管理的格式
# 或者直接编辑 .gitattributes
$ git lfs track "*.png"
# 添加所有需要追踪的文件类型（一次性添加多个扩展名）
$ git lfs track "**/*.{psd,ai,tiff,raw,sketch,mp4,mp3,zip,rar,sql,pdf}"

# 确认追踪规则 
$ git lfs track

# 查看当前 commit 有哪些文件被认为是 LFS 文件
$ git lfs ls-files

# 剪除存放于本地的 LFS 文件中那些旧版本的版本, 释放一些硬盘存储空间
$ git lfs prune

# 关闭
$ git lfs uninstall --local
```

 - & 参考资料：[Git LFS 大文件存储](https://blog.yusong.me/git/lfs)

### 关闭 Git 在 https 连接时对服务器证书的验证

```ad-warning
title: 场景
- ! 问题：OpenSSL SSL_read: Connection was reset, errno 10054
- 原因：这是服务器的 SSL 证书没有经过第三方机构的签署，所以报错。可全局执行：
```

```sh
$ git config --global http.sslVerify "false"
```

### Fatal: refusing to merge unrelated histories 解决

```sh
# 允许不相关历史提交，强制合并，然后本地处理冲突之后再进行提交
$ git pull origin master --allow-unrelated-histories

$ git pull --allow-unrelated-histories

$ git merge master --allow-unrelated-histories
```

### Husky > npm run -s precommit (node v 10. Xx. Xx)

```sh
$ git commit -m "提交页面备注" --no-verify
```

### 代码回滚误操作如何恢复

- 代码有进行 `commit` 操作

```sh
# 回滚上一个版本（删除工作空间的改动代码，撤销commit且撤销add）
$ git reset --hard HEAD^

# 如何恢复删除的代码
$ git reflog
$ git reset --hard [hash]
```

- 代码没有 `commit`，但进行了 `git add.`，解决方法参考 [链接](https://juejin.cn/post/6844903602981601294)

### 出现 git 提交冲突场景

```sh
# pull 和 push 同时存在
$ git pull --rebase
$ git rebase --continue

# 撤销 rebase 操作
$ git rebase --abort
```

### git merge 时避免或移除合并记录

##### 方式一

```sh
# 将 feature 分支的改动合并到当前分支，不产生合并记录
$ git merge --squash feature

# 需要手动 commit
$ git commit -m "feat: add feature"
```

##### 方式二

```sh
# 将 feature 分支的改动合并到 main 分支
# 切换到 feature 分支
$ git checkout feature

# rebase 到 main 分支
$ git rebase main

# 切回 main 分支，执行快进合并
$ git checkout main
$ git merge feature
```

### 下载源代码和仓库关联

```bash
# 方式一：
$ git push --force origin main

# 方式二（推荐）：
$ git pull origin main --allow-unrelated-histories
```
