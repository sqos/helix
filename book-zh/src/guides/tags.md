## 添加标签查询（Adding tags queries）

有关标签查询的更多背景信息，请参阅 tree-sitter 文档中的 [Code Navigation Systems](https://tree-sitter.github.io/tree-sitter/4-code-navigation.html)。

Helix 提供类似 LSP 的功能，例如文档和工作区符号选择器（document and workspace symbol pickers），对于具有基于语法树的 `tags.scm` 查询的语言可直接使用。要分析某种语言，该语言必须具备：

1. 一个 tree-sitter 语法解析器（grammar）
2. 一个 `tags.scm` 查询文件，该文件模式匹配语法树中感兴趣的节点

查询文件在贡献给 Helix 时应放置于：

```
runtime/queries/{language}/tags.scm
```

在本地测试时，也可以放在本地 runtime 目录下，例如 Linux 系统的：

```
~/.config/helix/runtime
```

### 支持的 Capture 名称

| Capture 名称             |
| ---------------------- |
| `definition.class`     |
| `definition.constant`  |
| `definition.function`  |
| `definition.interface` |
| `definition.macro`     |
| `definition.module`    |
| `definition.struct`    |
| `definition.type`      |

[示例查询文件](https://github.com/search?q=repo%3Ahelix-editor%2Fhelix+path%3A%2A%2A/tags.scm&type=Code) 可在 Helix GitHub 仓库中找到。
