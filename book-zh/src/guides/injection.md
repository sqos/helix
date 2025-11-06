## 添加注入（Injection）Queries

编写语言注入查询允许将特定节点标记为不同语言进行高亮显示。除了 tree-sitter 提供的[标准语言注入选项][upstream-docs]之外，Helix 还提供了一些扩展功能，可实现更精细的控制。

一个简单示例，将 Nix 中的所有字符串高亮为 Bash：

```scm
((string_expression (string_fragment) @injection.content)
  (#set! injection.language "bash"))
```

另一个示例，将注释中的链接和关键词如 "TODO" 高亮，复用专门的 "comment" 语言：

```scm
((comment) @injection.content
  (#set! injection.language "comment"))
```

## 捕获类型（Capture Types）

* `@injection.language`（标准）
  捕获节点可包含语言名称，用于高亮 `@injection.content` 捕获的节点。

* `@injection.content`（标准）
  标记需要根据 `@injection.language` 或其他注入设置高亮的内容。

* `@injection.filename`（扩展）
  捕获节点可包含带有已知扩展名的文件名，用以高亮 `@injection.content`。Helix 会使用默认 `languages.toml` 和用户自定义语言中定义的扩展名。

* `@injection.shebang`（扩展）
  捕获节点可包含 shebang，用于选择要高亮的语言。Helix 会使用默认及用户 `languages.toml` 中定义的 shebang。

## 设置（Settings）

* `injection.combined`（标准）
  指示树中所有匹配的节点应作为一个嵌套文档解析。

* `injection.language`（标准）
  强制将捕获的内容高亮为指定语言。

* `injection.include-children`（标准）
  指示内容节点的整个文本都应重新解析，包括其子节点的文本。默认情况下，子节点文本会被排除在注入文档之外。

* `injection.include-unnamed-children`（扩展）
  与 `injection.include-children` 类似，但仅对未命名的子节点有效。

## 谓词（Predicates）

* `#eq?`（标准）
  第一个参数（捕获）必须等于第二个参数（捕获或字符串）。

* `#match?`（标准）
  第一个参数（捕获）必须匹配第二个参数提供的正则表达式（字符串）。

* `#any-of?`（标准）
  第一个参数（捕获）必须是其他参数之一（字符串）。

[upstream-docs]: https://tree-sitter.github.io/tree-sitter/3-syntax-highlighting.html#language-injection
