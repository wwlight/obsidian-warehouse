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
