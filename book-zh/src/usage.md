# 使用 Helix

要获得 Helix 的完整交互式入门指南，请参阅
[tutor](https://github.com/helix-editor/helix/blob/master/runtime/tutor)，
可通过命令 `hx --tutor` 或 `:tutor` 访问。

> 💡 当前并非所有功能都有完整文档，请参考
> [快捷键映射](./keymap.md) 列表。

## 模式（Modes）

Helix 是一个**多模式编辑器**，意味着它有不同的模式来处理不同的任务。主要模式包括：

* [普通模式（Normal mode）](./keymap.md#normal-mode)：用于导航和执行编辑命令。这是默认模式。
* [插入模式（Insert mode）](./keymap.md#insert-mode)：用于直接输入文本。在普通模式下按下 `i` 进入。
* [选择/扩展模式（Select/extend mode）](./keymap.md#select--extend-mode)：用于进行选择并对选区执行操作。在普通模式下按下 `v` 进入。

## 缓冲区（Buffers）

缓冲区是文件在内存中的表示。你可以同时打开多个缓冲区。
使用 [选择器（pickers）](./pickers.md) 或命令如 `:buffer-next`、`:buffer-previous` 来打开或切换缓冲区。

## 先选择再编辑（Selection-first editing）

受 [Kakoune](http://kakoune.org/) 启发，Helix 遵循“**先选择 → 后操作**”的模型。
这意味着你要先选择要操作的对象（如单词、段落、行等），然后再执行动作（删除、更改、复制等）。
光标本质上就是一个单宽度的选区。

## 多重选择（Multiple selections）

同样受 Kakoune 启发，**多重选择**是 Helix 的核心交互方式之一。
例如，替换多个相同单词的标准方式是：
先选择所有实例（每个实例一个选区），
然后使用更改操作（`c`）即可同时编辑它们。

## 动作（Motions）

动作是用来**移动光标或修改选区**的命令，
用于导航或文本操作。
例如，`w` 用于移动到下一个单词，`f` 用于查找字符。
更多动作请参阅 [移动（Movement）](./keymap.md#movement) 部分。
