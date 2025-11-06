## 使用语法感知移动调整选区

在 Helix 中，`Alt-p`、`Alt-o`、`Alt-i` 和 `Alt-n`（或者 `Alt` + 方向键）允许你根据选区在语法树中的位置来移动选区。例如，许多语言中函数调用的语法如下：

```js
func(arg1, arg2, arg3);
```

Tree-sitter 可能会将函数调用解析成如下语法树：

```tsq
(call
  function: (identifier) ; func
  arguments:
    (arguments           ; (arg1, arg2, arg3)
      (identifier)       ; arg1
      (identifier)       ; arg2
      (identifier)))     ; arg3
```

使用 `:tree-sitter-subtree` 可以查看主选区的语法树。更直观的树状格式如下：

```
            ┌────┐
            │call│
      ┌─────┴────┴─────┐
      │                │
┌─────▼────┐      ┌────▼────┐
│identifier│      │arguments│
│  "func"  │ ┌────┴───┬─────┴───┐
└──────────┘ │        │         │
             │        │         │
   ┌─────────▼┐  ┌────▼─────┐  ┌▼─────────┐
   │identifier│  │identifier│  │identifier│
   │  "arg1"  │  │  "arg2"  │  │  "arg3"  │
   └──────────┘  └──────────┘  └──────────┘
```

假设你的选区包裹了 `arg1`（见上图），使用 `Alt-n` 将会选择语法树中下一个兄弟节点：`arg2`。

```js
// before
func([arg1], arg2, arg3)
// after
func(arg1, [arg2], arg3);
```

同样，`Alt-o` 会将选区扩展到父节点，在这个例子中就是 `arguments` 节点：

```js
func[(arg1, arg2, arg3)];
```

还有一些细微的行为可以避免你卡在没有兄弟节点的节点上。例如，当选区在 `arg1` 上使用 `Alt-p` 时，会选择前一个子节点；如果 `arg1` 没有前一个兄弟节点，选区会沿语法树向上移动，选择前一个元素。因此，在 `arg1` 上使用 `Alt-p` 将使选区移动到 `func` 的 `identifier` 节点。

[语言支持]: ./lang-support.md
