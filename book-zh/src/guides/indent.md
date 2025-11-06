## 添加缩进查询

Helix 使用 tree-sitter 来正确缩进新行。这需要一个 tree-sitter 语法以及一个 `indent.scm` 查询文件，放置在 `runtime/queries/{language}/indents.scm` 中。某行的缩进是通过从新行开头的最底层节点遍历语法树来计算的（参见 [Indent queries](#indent-queries)）。当某个节点被查询捕获时，它会对总缩进产生影响（具体方式取决于捕获名称）。

注意，新增缩进的起始位置很重要。例如，多个从同一行开始的缩进增加只会使总缩进级别增加 1。参见 [Capture types](#capture-types)。

默认情况下，Helix 使用 `hybrid` 缩进启发式。这意味着缩进查询不会用于计算某行的绝对预期缩进，而是用于计算新行与已存在行之间的预期缩进差。然后将此差值加到已存在行的实际缩进上。由于这会使缩进查询中的错误更难发现，建议在测试时通过 `:set indent-heuristic tree-sitter` 禁用该模式。本指南其余部分假设使用 `tree-sitter` 启发式。

## 缩进查询

当 Helix 通过 `o`、`O` 或 `<ret>` 插入新行时，为确定新行的缩进级别，会在文档上运行 `indents.scm` 中的查询。查询的起始位置为将要插入新行的上一行末尾。

对于 `o`，插入的行在光标下方，因此查询的起始位置是当前行的末尾。

```rust
fn need_hero(some_hero: Hero, life: Life) -> {
    matches!(some_hero, Hero { // ←─────────────────╮
        strong: true,//←╮  ↑  ↑                     │
        fast: true,  // │  │  ╰── query start       │
        sure: true,  // │  ╰───── cursor            ├─ traversal 
        soon: true,  // ╰──────── new line inserted │  start node
    }) &&            //                             │
//  ↑                                               │
//  ╰───────────────────────────────────────────────╯
    some_hero > life
}
```

对于 `O`，新插入的行是 *当前* 行，因此查询的起始位置是光标上一行的末尾。

```rust
fn need_hero(some_hero: Hero, life: Life) -> { // ←─╮
    matches!(some_hero, Hero { // ←╮          ↑     │
        strong: true,//    ↑   ╭───╯          │     │
        fast: true,  //    │   │ query start ─╯     │
        sure: true,  //    ╰───┼ cursor             ├─ traversal
        soon: true,  //        ╰ new line inserted  │  start node
    }) &&            //                             │
    some_hero > life //                             │
} // ←──────────────────────────────────────────────╯
```

从该起始节点开始，向上遍历语法树直至根节点。沿途收集每个缩进捕获，并根据其 [capture types](#capture-types) 和 [scopes](#scopes) 合并，得到该行的最终缩进级别。

### 捕获类型

* `@indent`（默认作用域 `tail`）：
  增加缩进级别 1。同一行中多次出现 *不* 累加。如果同一行同时存在至少一个 `@indent` 和一个 `@outdent` 捕获，则缩进级别保持不变。
* `@outdent`（默认作用域 `all`）：
  减少缩进级别 1。规则同 `@indent`。
* `@indent.always`（默认作用域 `tail`）：
  增加缩进级别 1。同一行中多次出现 *会* 累加。最终缩进级别为 `@indent.always` – `@outdent.always`。如果同一行同时有 `@indent` 和 `@indent.always`，则忽略 `@indent`。
* `@outdent.always`（默认作用域 `all`）：
  减少缩进级别 1。规则同 `@indent.always`。
* `@align`（默认作用域 `all`）：
  将此节点内的内容对齐到某个锚点。锚点由同一模式中 `@anchor` 捕获的节点起始位置提供。每个包含 `@align` 的模式应包含恰好一个 `@anchor`。低于（按起始行计算）`@align` 节点的节点的缩进（或反向缩进）会加到对齐所需的缩进中。
* `@extend`：
  将此节点的范围扩展到行末及比该节点起始行缩进更多的行。对于 Python 等语言有用，因为在缩进目的下，一些节点（如函数或类）也应包含其后的缩进行。
* `@extend.prevent-once`：
  阻止此节点的祖先的第一次扩展。例如，在 Python 中，return 表达式总是结束其所在块。注意，这只阻止下一次 `@extend` 捕获的扩展。如果捕获了多个祖先，仅阻止最内层祖先的扩展，其余祖先不受影响（无论最内层祖先是否本来会被扩展）。

#### `@indent` / `@outdent`

考虑这个例子：

```rust
fn shout(things: Vec<Thing>) {
    //                       ↑
    //                       ├───────────────────────╮ 缩进级别
    //                    @indent                    ├┄┄┄┄┄┄┄┄┄┄┄┄┄┄
    //                                               │
    let it_all = |out| { things.filter(|thing| { //  │      1
    //                 ↑                       ↑     │
    //                 ├───────────────────────┼─────┼┄┄┄┄┄┄┄┄┄┄┄┄┄┄
    //              @indent                 @indent  │
    //                                               │      2
        thing.can_do_with(out) //                    │
    })}; //                                          ├┄┄┄┄┄┄┄┄┄┄┄┄┄┄
  //↑↑↑                                              │      1
} //╰┼┴──────────────────────────────────────────────┴┄┄┄┄┄┄┄┄┄┄┄┄┄┄
// 3x @outdent
```

```scm
((block) @indent)
["}" ")"] @outdent
```

注意第二行，我们在同一行有两个块开始。在这种情况下，由于两个捕获发生在同一行，它们会合并，只产生净增加 1 的缩进。同样注意闭合的 `}` 是 `@indent` 捕获的一部分，但 3 个 `@outdent` 也合并成 1，使该行减少一个缩进级别。

#### `@extend` / `@extend.prevent-once`

考虑 Python 这种对空白敏感的语言时，`@extend` 的作用：

```scm
]
  (parenthesized_expression)
  (function_definition)
  (class_definition)
] @indent
```

```python
class Hero:
    def __init__(self, strong, fast, sure, soon):#  ←─╮
        self.is_strong = strong #                     │
        self.is_fast = fast     # ╭─── query start    │
        self.is_sure = sure     # │ ╭─ cursor         │
        self.is_soon = soon     # │ │                 │
        #     ↑            ↑      │ │                 │
        #     │            ╰──────╯ │                 │
        #     ╰─────────────────────╯                 │
        #                                             ├─ traversal
    def need_hero(self, life):         #              │  start node
        return (                       #              │
            self.is_strong             #              │
            and self.is_fast           #              │
            and self.is_sure           #              │
            and self.is_soon           #              │
            and self > life            #              │
        ) # ←─────────────────────────────────────────╯
```

没有大括号来捕获函数的作用域时，光标所在行的最小子节点会覆盖整个类内部。这样会错过整个函数节点及其缩进捕获，导致缩进级别少 1。

为解决此情况，`@extend` 告诉 Helix 将捕获节点的范围扩展到换行以及所有缩进级别大于该节点的连续行。

```scm
(parenthesized_expression) @indent

]
  (function_definition)
  (class_definition)
] @indent @extend
```

```python
class Hero:
    def __init__(self, strong, fast, sure, soon):#  ←─╮
        self.is_strong = strong #                     │
        self.is_fast = fast     # ╭─── query start    ├─ traversal
        self.is_sure = sure     # │ ╭─ cursor         │  start node
        self.is_soon = soon     # │ │ ←───────────────╯
        #     ↑            ↑      │ │                 
        #     │            ╰──────╯ │
        #     ╰─────────────────────╯
    def need_hero(self, life):
        return (
            self.is_strong
            and self.is_fast
            and self.is_sure
            and self.is_soon
            and self > life
        )
```

此外，有些情况下不希望扩展到所有缩进更大的行。考虑上面的 `need_hero` 函数，如果光标在返回表达式的最后一行：

```python
class Hero:
    def __init__(self, strong, fast, sure, soon):
        self.is_strong = strong
        self.is_fast = fast
        self.is_sure = sure
        self.is_soon = soon

    def need_hero(self, life):
        return (
            self.is_strong
            and self.is_fast
            and self.is_sure
            and self.is_soon
            and self > life
        ) # ←─── cursor
    #←────────── 光标在新行应到的位置
```

在 Python 中，有一些标记总是结束一个作用域，比如 return 语句。作用域结束时，缩进级别也应结束。但由于函数跨度被扩展到所有缩进更大的行，新行会继续保持同一缩进。`@outdent` 也无法解决，因为它会导致括号内的所有内容都减少缩进。

为解决此问题，需要标记扩展的结束。可以使用 `@extend.prevent-once`：

```scm
(parenthesized_expression) @indent

]
  (function_definition)
  (class_definition)
] @indent @extend

(return_statement) @extend.prevent-once
```

#### `@indent.always` / `@outdent.always`

如前所述，通常同一行有多个 `@indent` 或 `@outdent` 捕获时，它们会合并。

有时希望确保每个缩进捕获都累加，无论同一行出现多少次。例如在 YAML 中：

```yaml
  - foo: bar
# ↑ ↑
# │ ╰─────────────── map 起始
# ╰───────────────── list 元素起始
    baz: quux # ←─── 光标
    # ←───────── 新行光标应到位置
    garply: waldo
  - quux:
      bar: baz
    xyzzy: thud
    fred: plugh
```

在 YAML 中，经常有映射列表。在这种情况下，列表元素和映射都从同一行开始，但我们希望为每个元素增加缩进，使映射中的后续键相对于列表正确对齐。这时 `@indent.always` 就很有用。

```scm
((block_sequence_item) @item @indent.always @extend
  (#not-one-line? @item))

((block_mapping_pair
    key: (_) @key
    value: (_) @val
    (#not-same-line? @key @val)
  ) @indent.always @extend
)
```

## 谓词

在某些情况下，S 表达式无法准确表达应匹配的模式。为此，tree-sitter 允许谓词出现在模式的任意位置，类似 `#set!` 声明：

```scm
(some_kind
  (child_kind) @indent
  (#predicate? arg1 arg2 ...)
)
```

参数数量取决于使用的谓词。每个参数要么是捕获 (`@name`)，要么是字符串 (`"some string"`)。tree-sitter 支持以下谓词：

* `#eq?`/`#not-eq?`：
  第一个参数（捕获）必须/不能等于第二个参数（捕获或字符串）。

* `#match?`/`#not-match?`：
  第一个参数（捕获）必须/不能匹配第二个参数提供的正则（字符串）。

* `#any-of?`/`#not-any-of?`：
  第一个参数（捕获）必须/不能在其他参数（字符串）中。

另外，对于缩进查询，还支持一些自定义谓词：

* `#not-kind-eq?`：
  第一个参数（捕获）的类型不得等于第二个参数（字符串）。

* `#same-line?`/`#not-same-line?`：
  两个参数提供的捕获必须/不得在同一行开始。

* `#one-line?`/`#not-one-line?`：
  第一个参数提供的捕获必须/不得仅跨一行。

### 作用域

新增缩进并不总是应用于整个节点。例如，大多数情况下，当一个节点应缩进时，我们实际上只希望除了首行外的内容缩进。为此，有几个作用域（未来可根据需要添加更多作用域）：

* `tail`：
  此作用域适用于捕获节点的除首行以外的所有内容。

* `all`：
  此作用域适用于整个捕获节点。仅当捕获节点是其所在行的第一个节点时，与 `tail` 不同。

例如，假设我们有如下函数：

```rust
fn aha() { // ←─────────────────────────────────────╮
  let take = "on me";  // ←──────────────╮  作用域:  │
  let take = "me on";             //     ├─ "tail"  ├─ (block) @indent
  let ill = be_gone_days(1 || 2); //     │          │
} // ←───────────────────────────────────┴──────────┴─ "}" @outdent
                                         //                作用域: "all"
```

我们可以使用 `#set!` 声明写如下查询：

```scm
((block) @indent
 (#set! "scope" "tail"))
("}" @outdent
 (#set! "scope" "all"))
```

如图所示，`"tail"` 作用域覆盖节点，首行除外。到闭合大括号为止的所有行都会增加 1 个缩进级别。然后在闭合大括号上，我们遇到一个作用域为 `"all"` 的 outdent，这意味着首行也包含在内，该行的缩进级别被抵消。（注意这些作用域是 `@indent` 和 `@outdent` 的默认值——这里显式写出仅用于演示。）
