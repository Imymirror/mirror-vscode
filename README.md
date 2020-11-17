# Table of Content
- [Table of Content](#table-of-content)
- [简介](#简介)
- [速查表](#速查表)
- [如何使用我的配置?](#如何使用我的配置)
- [我对 VSCode 做了哪些配置](#我对-vscode-做了哪些配置)
  - [`ctrl + hjkl`导航栏跳](#ctrl--hjkl导航栏跳)
  - [`H,L` 替代 `^$`](#hl-替代-)
  - [j/k 会打开折叠问题的修复](#jk-会打开折叠问题的修复)
  - [markdown preview](#markdown-preview)
  - [基于 VSCodeVim 和 Which-key 的类 Spacemacs 绑定](#基于-vscodevim-和-which-key-的类-spacemacs-绑定)
  - [easymotion](#easymotion)
- [一些问题的解决方案](#一些问题的解决方案)
  - [vscodevim 解决英文输入法长按不打印多个字母](#vscodevim-解决英文输入法长按不打印多个字母)
- [插件推荐](#插件推荐)
  - [PasteURL](#pasteurl)
  - [PasteImage](#pasteimage)
- [使用技巧 (tips and tricks)](#使用技巧-tips-and-tricks)
  - [VSCodeVim](#vscodevim)

# 简介

mirror-vscode 是关于 VSCode 使用过程中积累的一份详细备忘录.

mirror-vscode 是基于个人使用习惯的一份 VSCode 配置.

由于重度依赖 vim 的操作方式来提高编辑文本的效率, 所以 mirror-vscode 也是基于 [VSCodeVim](https://github.com/VSCodeVim/Vim) 和 [vscode-which-key](https://github.com/VSpaceCode/vscode-which-key) 的一份 vim 配置方案. 

# 速查表

[VSCodeVim 提供了 Vim 的基础功能 ROADMAP](https://github.com/VSCodeVim/Vim/blob/master/ROADMAP.md)

[Gist cloudSettings](https://gist.github.com/Imymirror/df3b3a5e832c1f3cb7423786836d6abd#file-settings-json-L1) : 我通过 [vscode Setting Sync](https://github.com/shanalikhan/code-settings-sync) 插件导出一份公开的配置.
默认 Leader key 是 `<space>`, 
![](Image/README/2020-11-17-12-04-20.png)

# 如何使用我的配置?

如果你想直接使用我的配置, 有两种方案:

1. 使用 [Setting Sync](https://github.com/shanalikhan/code-settings-sync) 插件 : 推荐. 这种方式会将 **配置文件连同插件** 一起下载, 过程完全自动化. 只需等待一小会,环境即搭建完成 
    - 从应用商店下载 `Setting Sync` 插件 
    - `ctrl + shift + p`, `sync:Advanced Options` -> `sync:Open Settings`, `Environment Settings` 填入 我的 public Gist ID `df3b3a5e832c1f3cb7423786836d6abd`.
    - `ctrl + shift + p`, `sync: Download Setting`

2. 从公开的 [Gist cloudSettings](https://gist.github.com/Imymirror/df3b3a5e832c1f3cb7423786836d6abd) 上面复制黏贴相关配置到你的本地配置文件中(主要是 `setting.json`)

# 我对 VSCode 做了哪些配置
## `ctrl + hjkl`导航栏跳

`keybindings.json`:
```json
  {
    "key": "ctrl+h",
    "command": "workbench.action.navigateLeft"
  },
  {
    "key": "ctrl+l",
    "command": "workbench.action.navigateRight"
  },
  {
    "key": "ctrl+k",
    "command": "workbench.action.navigateUp"
  },
  {
    "key": "ctrl+j",
    "command": "workbench.action.navigateDown"
  },
```

## `H,L` 替代 `^$`

`setting.json` : 

```json
{
  "before": [
    "L"
  ],
  "after": [
    "$"
  ]
},
{
  "before": [
    "H"
  ],
  "after": [
    "^"
  ]
},
```

## j/k 会打开折叠问题的修复

```json
    // gj gk
    {
      "before": [
        "j"
      ],
      "after": [
        "g",
        "j"
      ]
    },
    {
      "before": [
        "k"
      ],
      "after": [
        "g",
        "k"
      ]
    },
```

## markdown preview

关闭 `preview 滚动的时候, Markdown 文件跟着滚动`
```json
  "markdown.preview.scrollEditorWithPreview": false,
```

## 基于 VSCodeVim 和 Which-key 的类 Spacemacs 绑定 

安装 [VSCodeVim](https://github.com/VSCodeVim/Vim) 后, vscode就拥有了vim的基础功能. 见 [ROADMAP](https://github.com/VSCodeVim/Vim/blob/master/ROADMAP.md)

安装 [vscode-which-key](https://github.com/VSpaceCode/vscode-which-key) 之后, 就会有一份 [默认的keybinding](https://vspacecode.github.io/docs/default-keybindings).

我覆盖了 `which-key`  [默认的keybinding](https://vspacecode.github.io/docs/default-keybindings). 根据自己的习惯绑定了一份. 我会根据需要去增减 keybinding, 实际上是 `默认绑定的阉割修改版+自己的绑定`. 

如果想使用 **`which-key`  [默认的keybinding](https://vspacecode.github.io/docs/default-keybindings)** , 很简单, 只需要注释掉 `setting.json` 中的 `whichkey.bindings` 字段: 

```json
"whichkey.bindings": [

  // lots of keybindings here
  // ...

]
```

##  easymotion

|   key   |       Description       |
| :-----: | :---------------------: |
| gs<SPC> | Search by one character |
|   gsj   | Start of line forwards  |
|   gsk   | Start of line backwards |
|   gsw   | Start of word forwards  |
|   gsb   | Start of word backwards |


# 一些问题的解决方案
## vscodevim 解决英文输入法长按不打印多个字母

在 Terminal 里执行下列指令, 并重启 VSCode:
```
$ defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false         # For VS Code
$ defaults write com.microsoft.VSCodeInsiders ApplePressAndHoldEnabled -bool false # For VS Code Insider
$ defaults delete -g ApplePressAndHoldEnabled  
```

如果你使用的是VSCodium, 在终端执行以下语句, 重启VSCode
```
$ defaults write com.visualstudio.code.oss ApplePressAndHoldEnabled -bool false
```

# 插件推荐

## PasteURL

[marketplace PasteURL](https://marketplace.visualstudio.com/items?itemName=kukushi.pasteurl)

在 Markdown 中使用, 复制一个 URL 到剪贴板, Hit "Command + Shift + P" and then type Paste URL and hit enter. 会在当前光标位置生成 Markdown 风格的 Link.

我绑定了快捷键 `<space> a u`

## PasteImage

[marketplace PasteImage](https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image)

在 Markdown 中, 使用截图工具截取屏幕到剪贴板中, `Cmd+Alt+V`, 自动将剪贴板中的截图保存到当前文件的同一层级目录的 `Image/`下.

我绑定了快捷键 `<space> a i`


# 使用技巧 (tips and tricks)

## VSCodeVim