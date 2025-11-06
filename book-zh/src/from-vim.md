# 从 Vim 迁移

Helix 的编辑模型深受 Vim 和 Kakoune 的启发，一个显著的区别（也是与 Kakoune 最相似的地方）是 Helix 遵循 `selection → action` 模型。
这意味着你要操作的对象（单词、段落、行等）先被选中，然后再执行操作（删除、修改、复制等）。光标仅仅表示单个宽度的选择。

另请参见 Kakoune 的 [从 Vim 迁移](https://github.com/mawww/kakoune/wiki/Migrating-from-Vim) 以及 Helix 的 [从 Vim 迁移](https://github.com/helix-editor/helix/wiki/Migrating-from-Vim)。

> TODO: 提及 textobjects、surround、寄存器（registers）
