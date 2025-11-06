## 添加 Textobject 查询（Adding textobject queries）

Helix 支持语言特定的 textobjects，例如函数、类等。
这些 textobjects 需要配套的 tree-sitter 语法解析器和 `textobjects.scm` 查询文件才能正常工作。Tree-sitter 允许我们查询源代码的语法树并捕获其中的特定部分。查询文件使用 Lisp 方言编写。
有关如何编写查询的更多信息，请参阅 [官方 tree-sitter 文档][tree-sitter-queries]。

在贡献给 Helix 时，查询文件应放置于：

```
runtime/queries/{language}/textobjects.scm
```

在本地测试查询文件时，可将其放在本地 runtime 目录，例如 Linux 系统的：

```
~/.config/helix/runtime
```

### 支持的 Capture 名称

| Capture 名称           |
| -------------------- |
| `function.inside`    |
| `function.around`    |
| `class.inside`       |
| `class.around`       |
| `test.inside`        |
| `test.around`        |
| `parameter.inside`   |
| `parameter.around`   |
| `comment.inside`     |
| `comment.around`     |
| `entry.inside`       |
| `entry.around`       |
| `xml-element.inside` |
| `xml-element.around` |

[示例查询文件][textobject-examples] 可在 Helix GitHub 仓库中找到。

### 基于 textobject 的导航查询

在 Helix 中，基于 tree-sitter 的导航使用以下捕获顺序：

* `object.movement`
* `object.around`
* `object.inside`

例如，如果某语言的 `textobjects.scm` 文件已经定义了 `function.around` 捕获，函数导航就会自动可用。
只有当 `function.around` 捕获的节点在导航上下文中不合适时，才需要定义 `function.movement`。

[tree-sitter-queries]: https://tree-sitter.github.io/tree-sitter/using-parsers/queries/1-syntax.html
[tree-sitter-captures]: https://tree-sitter.github.io/tree-sitter/using-parsers/queries/2-operators.html#capturing-nodes
[textobject-examples]: https://github.com/search?q=repo%3Ahelix-editor%2Fhelix+path%3A%2A%2A/textobjects.scm&type=Code&ref=advsearch&l=&l=
