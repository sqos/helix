## Surround（环绕操作）

Helix 内置了类似于 [vim-surround](https://github.com/tpope/vim-surround) 的功能。其快捷键设计灵感来源于 [vim-sandwich](https://github.com/machakann/vim-sandwich)：

![Surround demo](https://user-images.githubusercontent.com/23398472/122865801-97073180-d344-11eb-8142-8f43809982c6.gif)

| 快捷键序列                           | 功能           |
| ------------------------------- | ------------ |
| `ms<char>`（选中文本后）               | 给选中的文本添加环绕字符 |
| `mr<char_to_replace><new_char>` | 替换最接近的环绕字符   |
| `md<char_to_delete>`            | 删除最接近的环绕字符   |

你可以使用计数（counts）对外层括号进行操作。

Surround 也可以作用于多重选区。例如，将文件中每个 `(use)` 改为 `[use]`：

1. 使用 `%` 选择整个文件
2. 使用 `s` 按搜索词拆分选区
3. 输入 `use` 并按 Enter
4. 使用 `mr([` 将括号替换为方括号

目前还不支持多字符环绕，但计划在未来版本中加入。
