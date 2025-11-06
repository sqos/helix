# 添加彩虹括号（Rainbow Bracket）查询

Helix 使用 `rainbows.scm` 的 tree-sitter 查询文件来实现彩虹括号功能。

Tree-sitter 查询的详细文档可参考官方在线文档。如果你是第一次编写查询，请查看[语法高亮查询]和[查询语法]相关章节。

彩虹查询有两个捕获（capture）：`@rainbow.scope` 和 `@rainbow.bracket`。

* `@rainbow.scope` 应该捕获增加嵌套层级的节点；
* `@rainbow.bracket` 应该捕获括号节点。

换句话说：`@rainbow.scope` 会为其下所有节点切换到下一个彩虹颜色，而 `@rainbow.bracket` 会将捕获的节点用当前彩虹颜色进行渲染。

---

## 示例：为 TSQ 添加彩虹查询

将查询文件放置在仓库根目录的：

```
runtime/queries/tsq/rainbows.scm
```

### 1. 添加 `@rainbow.bracket` 捕获

TSQ 仅包含圆括号和方括号：

```tsq
["(" ")" "[" "]"] @rainbow.bracket
```

注意：方括号内节点的顺序无影响。

> 为什么这些节点要加引号？
> 大多数语法高亮会捕获括号包裹的文本，这些是 *命名节点*，对应语法规则中的名称。括号通常在 tree-sitter 语法中写为字面字符串，例如：
>
> ```js
> {
>   arguments: seq("(", repeat($.argument), ")"),
> }
> ```
>
> 在查询中，tree-sitter 可以用相同的字面字符串捕获这些节点。

---

### 2. 添加 `@rainbow.scope` 捕获

查看 `grammar.js` 文件可以帮助确定哪些节点应切换彩虹颜色。以 TSQ 为例，[grammar.js 文件][tsq grammar.js] 中：

* `(alternation)` (L36)
* `(group)` (L57)
* `(named_node)` (L59)
* `(predicate)` (L87)
* `(wildcard_node)` (L97)

这些节点包含括号或方括号，并且是括号的直接父节点，因此我们将它们捕获为 `@rainbow.scope`：

```tsq
[
  (group)
  (named_node)
  (wildcard_node)
  (predicate)
  (alternation)
] @rainbow.scope
```

> 这种策略适用于大多数编程和配置语言。标记语言（如 HTML、XML）可能需要额外实验来确定正确的 scope 和 bracket 节点。

命令 `:tree-sitter-subtree` 可显示主光标下的语法树，有助于确定查询写法。

---

### 3. 属性（Properties）

`rainbow.include-children` 属性可应用于 `@rainbow.scope` 捕获。

默认情况下，`@rainbow.bracket` 必须是 `@rainbow.scope` 捕获节点的直接子节点才能高亮。设置 `rainbow.include-children` 后，即使是间接子节点，也可高亮。

例如在 HTML 中：

语法树：

```tsq
(element                   ; <a>link</a>
  (start_tag               ; <a>
    (tag_name))            ; a
  (text)                   ; link
  (end_tag                 ; </a>
    (tag_name)))           ; a
```

* 将 `<`、`>`、`</` 捕获为 `@rainbow.bracket`：

```tsq
["<" ">" "</"] @rainbow.bracket
```

* 将 `(element)` 捕获为 `@rainbow.scope`，因为元素节点嵌套可增加层级：

```tsq
(element) @rainbow.scope
```

但是 `<`、`>`、`</` 并非 `(element)` 的直接子节点，因此无法高亮。通过设置属性解决：

```tsq
((element) @rainbow.scope
 (#set! rainbow.include-children))
```

> 对绝大多数编程语言而言，不需要 `rainbow.include-children`。仅在嵌套层级节点并非括号的直接父节点时才需使用。

[语法高亮查询]: https://tree-sitter.github.io/tree-sitter/syntax-highlighting#highlights
[查询语法]: https://tree-sitter.github.io/tree-sitter/using-parsers#pattern-matching-with-queries
[tsq grammar.js]: https://github.com/the-mikedavis/tree-sitter-tsq/blob/48b5e9f82ae0a4727201626f33a17f69f8e0ff86/grammar.js
