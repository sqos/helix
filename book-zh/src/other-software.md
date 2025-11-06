# 其他软件中的 Helix 模式

Helix 的键位映射和交互模型（[使用 Helix](#usage.md)）如果能在多种编辑环境中一致使用，将更易于采纳。然而，某些使用场景无法直接在 Helix 中轻松实现。类似于 Vim，这导致在各种其他软件中创建了“Helix 模式”，以便在更多场景中实现 Helix 风格的编辑。

“Helix 模式”通常仍处于早期阶段或完全缺失。对于这种情况，我们也会链接相关的 bug 或讨论。

## 其他编辑器

| 编辑器  | 提供 Helix 编辑的插件或功能  | 备注 |
| --------------------------------------------------------------------------------------------------------- | -------- | -------|
| [Vim](https://www.vim.org/) | [helix.vim](https://github.com/chtenb/helix.vim) 配置  | |
| [IntelliJ IDEA](https://www.jetbrains.com/idea/) / [Android Studio](https://developer.android.com/studio) | [IdeaVim](https://plugins.jetbrains.com/plugin/164-ideavim) 插件 + [helix.idea.vim](https://github.com/chtenb/helix.vim) 配置 | 推荐最低版本 IdeaVim 2.19.0 |
| [Visual Studio](https://visualstudio.microsoft.com/) | [VsVim](https://marketplace.visualstudio.com/items?itemName=JaredParMSFT.VsVim) 插件 + [helix.vs.vim](https://github.com/chtenb/helix.vim) 配置  | |
| [Visual Studio Code](https://code.visualstudio.com/) | [Dance](https://marketplace.visualstudio.com/items?itemName=gregoire.dance) 扩展，或其 [Helix 分支](https://marketplace.visualstudio.com/items?itemName=kend.dancehelixkey) | Helix 分支已发生分叉。也可使用原 Dance 并直接调整其键位绑定（参考 [此配置](https://github.com/71/dance/issues/299#issuecomment-1655509531)） |
| [Visual Studio Code](https://code.visualstudio.com/) | [Helix for VS Code](https://marketplace.visualstudio.com/items?itemName=jasew.vscode-helix-emulation) 扩展 | |
| [Zed](https://zed.dev/) | 原生通过键位绑定 ([Bug](https://github.com/zed-industries/zed/issues/4642)) | |
| [CodeMirror](https://codemirror.net/) | [codemirror-helix](https://gitlab.com/_rvidal/codemirror-helix) ||
| [Lite XL](https://lite-xl.com/) | [lite-modal-hx](https://codeberg.org/Mandarancio/lite-modal-hx) |  |
| [Lapce](https://lap.dev/lapce/) | | 请求链接: [https://github.com/lapce/lapce/issues/281](https://github.com/lapce/lapce/issues/281) |

## Shell

| Shell   | 提供 Helix 编辑的插件或功能                                                                                                   |
| ------- | ------------------------------------------------------------------------------------------------------------------- |
| Fish    | [功能请求](https://github.com/fish-shell/fish-shell/issues/7748)                                                        |
| Fish    | [fish-helix](https://github.com/sshilovsky/fish-helix/tree/main)                                                    |
| Zsh     | [helix-zsh](https://github.com/john-h-k/helix-zsh) 或 [zsh-helix-mode](https://github.com/Multirious/zsh-helix-mode) |
| Nushell | [功能请求](https://github.com/nushell/reedline/issues/639)                                                              |

## 其他软件

| 软件                               | 提供 Helix 编辑的插件或功能                                           | 备注                         |
| -------------------------------- | ----------------------------------------------------------- | -------------------------- |
| [Obsidian](https://obsidian.md/) | [Obsidian-Helix](https://github.com/Sinono3/obsidian-helix) | 使用上文列出的 `codemirror-helix` |
