#mac #备忘录 #快捷键

### 查看 wifi 密码

```sh
$ sudo security find-generic-password -ga "无线网名称" | grep "password"
```

### 防止生成.DS_Store 的命令和恢复方法

```sh
# 禁止生成 .DS_Store
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool TRUE
defaults write com.apple.desktopservices DSDontWriteUSBStores -bool TRUE

# 删除现有的 .DS_Store 文件
find . -name ".DS_Store" -delete

# 如果之后需要恢复默认设置，可以运行：
defaults delete com.apple.desktopservices DSDontWriteNetworkStores
defaults delete com.apple.desktopservices DSDontWriteUSBStores
```

### app 取消证书校验

```sh
# 终端输入
$ xattr -r -d com.apple.quarantine [app路径（直接拖入）]
```

### 终端快捷键

| **功能** | **快捷键**     |
| ------ | ----------- |
| 快速清屏   | clear、⌘ + k |

### 系统快捷键

| **功能**         | **快捷键**                                  |
| -------------- | ---------------------------------------- |
| 快速清除废纸篓        | shift + option + ⌘ + delete(无 shift 有弹框) |
| 强制退出应用程序框      | esc + option + ⌘                         |
| 切换隐藏文件夹        | ⌘ + shift +.                             |
| 系统截图、录像        | ⌘ + shift + 4/5                          |
| 程序坞切换隐藏        | ⌘ + option + d                           |
| 打开系统 Emoji     | ctrl + ⌘ + 空格｜fn                         |
| 在 访达 中，搜索文件路径  | ⌘ + shift + g                            |
| 最小化应用          | ⌘ + m                                    |
| 预览文件 \| 全屏预览文件 | 空格｜空格 + option                           |

### 小技巧

- 长按 `option` 键，点击程序坞图标，快速切换应用显示；
- 长按 `option` 键，点击顶部菜单栏 Wi-Fi，可查看详情信息；
- 长按 `option` 键，右键菜单；
- 长按 `option` 键，快速拖拽文件复制；
- 长按 `option` 键，快速切换文件展开；
- 长按 `⌘` 键，点击顶部菜单栏可对图标排序；
