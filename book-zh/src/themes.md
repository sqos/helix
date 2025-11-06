## 主题

要使用主题，在你的 [`config.toml`](./configuration.md) 文件顶部添加 `theme = "<name>"`，或者在运行时使用 `:theme <name>` 选择主题。

可以为浅色模式和深色模式配置不同的主题。在支持 [模式 2031 深/浅检测](https://github.com/contour-terminal/contour/blob/master/docs/vt-extensions/color-palette-update-notifications.md) 的终端中，主题模式会根据终端自动检测。

```toml
[theme]
dark = "catppuccin_frappe"
light = "catppuccin_latte"
## 可选。如果终端未声明偏好，则使用此项。
## 如果未指定，默认使用 `dark` 的主题。
# fallback = "catppuccin_frappe"
```

## 创建主题

创建一个以主题名命名的文件（例如 `mytheme.toml`），并将其放入 `themes` 目录中（Linux/Mac：`~/.config/helix/themes`，Windows：`%AppData%\helix\themes`）。目录可能需要提前创建。

> 💡 “default”和“base16_default”是内置主题的保留名称，用户定义的主题无法覆盖。

### 概述

主题文件中的每一行格式如下：

```toml
key = { fg = "#ffffff", bg = "#000000", underline = { color = "#ff0000", style = "curl"}, modifiers = ["bold", "italic"] }
```

其中，`key` 表示要设置样式的对象，`fg` 指定前景色，`bg` 指定背景色，`underline` 指定下划线样式/颜色，`modifiers` 是样式修饰符列表。`bg`、`underline` 和 `modifiers` 可省略以使用默认值。

只指定前景色示例：

```toml
key = "#ffffff"
```

如果 key 中包含点 `'.'`，必须加引号，以防被解析为 [dotted key](https://toml.io/en/v1.0.0#keys)。

```toml
"key.key" = "#ffffff"
```

可以参考默认的 `theme.toml`：[链接](https://github.com/helix-editor/helix/blob/master/theme.toml)
用户提交的主题：[链接](https://github.com/helix-editor/helix/blob/master/runtime/themes)。

## 主题创建细节

### 颜色调色板

建议定义命名颜色调色板，并在主题配置中引用。可在主题文件中添加 `palette` 表：

```toml
"ui.background" = "white"
"ui.text" = "black"

[palette]
white = "#ffffff"
black = "#000000"
```

注意 `[palette]` 表包含其头部后的所有键，因此应放在普通主题选项之后。

默认调色板使用终端的 16 色，颜色名称如下。配置文件中的 `[palette]` 部分会覆盖默认调色板并进行合并。

| 颜色名称            |
| --------------- |
| `default`       |
| `black`         |
| `red`           |
| `green`         |
| `yellow`        |
| `blue`          |
| `magenta`       |
| `cyan`          |
| `gray`          |
| `light-red`     |
| `light-green`   |
| `light-yellow`  |
| `light-blue`    |
| `light-magenta` |
| `light-cyan`    |
| `light-gray`    |
| `white`         |

### 修饰符

支持的终端修饰符如下：

| 修饰符           |
| ------------- |
| `bold`        |
| `dim`         |
| `italic`      |
| `underlined`  |
| `slow_blink`  |
| `rapid_blink` |
| `reversed`    |
| `hidden`      |
| `crossed_out` |

> 💡 `underlined` 修饰符已弃用，仅为向后兼容。其行为等同于设置 `underline.style="line"`。

### 下划线样式

`underline.style` 可使用下列值（需终端支持）：

| 样式            |
| ------------- |
| `line`        |
| `curl`        |
| `dashed`      |
| `dotted`      |
| `double_line` |

## 主题继承与彩虹高亮

### 继承

可以通过 `inherits` 属性继承已有主题，并在此基础上覆盖特定样式或调色板：

```toml
inherits = "boo_berry"

# 覆盖关键字颜色
"keyword" = { fg = "gold" }

# 覆盖调色板颜色
[palette]
berry = "#2A2A4D"
```

### 彩虹括号

`rainbow` 键用于匹配括号的彩虹高亮，值为样式列表：

```toml
rainbow = ["#ff0000", "#ffa500", "#fff000", { fg = "#00ff00", modifiers = ["bold"] }]
```

可以使用调色板中的颜色和修饰符。

---

## Scope（作用域）

主题文件可使用的作用域（scope）分为两类：语法高亮与界面元素。

### 语法高亮

这些作用域对应 [tree-sitter scopes](https://tree-sitter.github.io/tree-sitter/3-syntax-highlighting.html#highlights)。匹配样式时，优先使用最长匹配的主题键。例如 `function.builtin.static` 会匹配 `function.builtin` 而不是 `function`。

类似 Sublime Text 的 scope 命名规范，参考 [TextMate](https://macromates.com/manual/en/language_grammars)。

#### 主要语法作用域示例

* **attribute**：类属性、HTML 标签属性
* **type**：

  * `builtin`：语言内置类型（`int`, `usize`）
  * `parameter`：泛型类型参数（`T`）
  * `enum`：

    * `variant`
  * `constructor`
* **constant**：

  * `builtin`：内置常量 (`true`, `false`, `nil`)
  * `character`

    * `escape`
  * `numeric`：

    * `integer`
    * `float`
* **string**：

  * `regexp`
  * `special`：

    * `path`
    * `url`
    * `symbol`（Erlang/Elixir atoms，Ruby symbols）
* **comment**：

  * `line`：

    * `documentation`
  * `block`：

    * `documentation`
  * `unused`：未使用变量或模式 `_`、`_foo`
* **variable**：

  * `builtin`：保留变量 (`self`, `this`)
  * `parameter`
  * `other`：

    * `member`：

      * `private`
* **label**：CSS 类名 `.class` 或 ID `#id`
* **punctuation**：

  * `delimiter`：逗号、冒号
  * `bracket`：括号
  * `special`：字符串插值括号
* **keyword**：

  * `control`：条件、循环、导入、返回、异常
  * `operator`：逻辑或运算符
  * `directive`：预处理器指令
  * `function`：函数关键字
  * `storage`：存储相关关键字
* **operator**：`||`, `+=`, `>` 等
* **function**：

  * `builtin`
  * `method`：

    * `private`
  * `macro`
  * `special`：C 预处理器
* **tag**：HTML 标签

  * `builtin`
* **namespace**
* **special**：如 Rust 的 `derive`
* **markup**：

  * `heading`：标题

    * `marker`
    * `1` ~ `6`
  * `list`：列表

    * `numbered`, `unnumbered`, `checked`, `unchecked`
  * `bold`, `italic`, `strikethrough`
  * `link`：

    * `url`, `label`, `text`
  * `quote`
  * `raw`：

    * `inline`, `block`
* **diff**：版本控制变化

  * `plus`, `minus`, `delta` 与对应 gutter 指示器

### 界面（Interface）

用于编辑器界面主题，例如弹出窗口、提示等：

* `markup`：

  * `normal`：

    * `completion`：自动补全文档弹窗
    * `hover`：悬浮提示
  * `heading`：

    * `completion`
    * `hover`
  * `raw.inline`：

    * `completion`
    * `hover`

| Key                               | 说明                                             |
| --------------------------------- | ---------------------------------------------- |
| `ui.background`                   |                                                |
| `ui.background.separator`         | 输入行下方的选择器分隔符                                   |
| `ui.cursor`                       |                                                |
| `ui.cursor.normal`                |                                                |
| `ui.cursor.insert`                |                                                |
| `ui.cursor.select`                |                                                |
| `ui.cursor.match`                 | 匹配括号等                                          |
| `ui.cursor.primary`               | 主光标                                            |
| `ui.cursor.primary.normal`        |                                                |
| `ui.cursor.primary.insert`        |                                                |
| `ui.cursor.primary.select`        |                                                |
| `ui.debug.breakpoint`             | 断点指示器，在 gutter 中显示                             |
| `ui.debug.active`                 | 调试暂停时当前行的指示器，在 gutter 中显示                      |
| `ui.gutter`                       | gutter                                         |
| `ui.gutter.selected`              | 光标所在行的 gutter                                  |
| `ui.linenr`                       | 行号                                             |
| `ui.linenr.selected`              | 光标所在行的行号                                       |
| `ui.statusline`                   | 状态栏                                            |
| `ui.statusline.inactive`          | 状态栏（未聚焦文档）                                     |
| `ui.statusline.normal`            | 普通模式下的状态栏（仅当启用 `editor.color-modes` 时有效）       |
| `ui.statusline.insert`            | 插入模式下的状态栏（仅当启用 `editor.color-modes` 时有效）       |
| `ui.statusline.select`            | 选择模式下的状态栏（仅当启用 `editor.color-modes` 时有效）       |
| `ui.statusline.separator`         | 状态栏中的分隔符                                       |
| `ui.bufferline`                   | buffer line 样式                                 |
| `ui.bufferline.active`            | buffer line 中的活动 buffer 样式                     |
| `ui.bufferline.background`        | buffer line 背景样式                               |
| `ui.popup`                        | 文档弹窗（例如 Space + k）                             |
| `ui.popup.info`                   | 多键选项的提示                                        |
| `ui.picker.header`                | 多列选择器的头部行                                      |
| `ui.picker.header.column`         | 多列选择器中的列名                                      |
| `ui.picker.header.column.active`  | 多列选择器中光标所在的列名                                  |
| `ui.window`                       | 分割窗口的边界线                                       |
| `ui.help`                         | 命令说明框                                          |
| `ui.text`                         | 默认文本样式，包括命令提示、弹窗文本等                            |
| `ui.text.focus`                   | picker 中当前选中行                                  |
| `ui.text.inactive`                | 与 `ui.text` 相同，但用于非活动文本（如建议列表中）                |
| `ui.text.info`                    | `ui.popup.info` 中的 key: 命令文本                   |
| `ui.text.directory`               | 提示完成中的目录名                                      |
| `ui.virtual.ruler`                | 标尺列（参见 [`editor.rulers` 配置]）                   |
| `ui.virtual.whitespace`           | 可见空白字符                                         |
| `ui.virtual.indent-guide`         | 垂直缩进指示线                                        |
| `ui.virtual.inlay-hint`           | 所有类型 inlay hints 的默认样式                         |
| `ui.virtual.inlay-hint.parameter` | `parameter` 类型的 inlay hints 样式（语言服务器无需设置 kind） |
| `ui.virtual.inlay-hint.type`      | `type` 类型的 inlay hints 样式（语言服务器无需设置 kind）      |
| `ui.virtual.wrap`                 | 软换行指示符（参见 [`editor.soft-wrap` 配置]）             |
| `ui.virtual.jump-label`           | 虚拟跳转标签样式                                       |
| `ui.menu`                         | 代码和命令补全菜单                                      |
| `ui.menu.selected`                | 被选中的自动补全项                                      |
| `ui.menu.scroll`                  | 滚动条样式，`fg` 设置滑块颜色，`bg` 设置轨道颜色                  |
| `ui.selection`                    | 编辑区选中区域                                        |
| `ui.selection.primary`            |                                                |
| `ui.highlight`                    | picker 预览中的高亮行                                 |
| `ui.highlight.frameline`          | 调试暂停时的当前行                                      |
| `ui.cursorline.primary`           | 主光标所在行（如果启用了 cursorline）                       |
| `ui.cursorline.secondary`         | 其他光标所在行（如果启用了 cursorline）                      |
| `ui.cursorcolumn.primary`         | 主光标所在列（如果启用了 cursorcolumn）                     |
| `ui.cursorcolumn.secondary`       | 其他光标所在列（如果启用了 cursorcolumn）                    |
| `warning`                         | Diagnostics warning（gutter）                    |
| `error`                           | Diagnostics error（gutter）                      |
| `info`                            | Diagnostics info（gutter）                       |
| `hint`                            | Diagnostics hint（gutter）                       |
| `diagnostic`                      | Diagnostics 回退样式（编辑区）                          |
| `diagnostic.hint`                 | Diagnostics hint（编辑区）                          |
| `diagnostic.info`                 | Diagnostics info（编辑区）                          |
| `diagnostic.warning`              | Diagnostics warning（编辑区）                       |
| `diagnostic.error`                | Diagnostics error（编辑区）                         |
| `diagnostic.unnecessary`          | 带 unnecessary 标签的 Diagnostics（编辑区）             |
| `diagnostic.deprecated`           | 带 deprecated 标签的 Diagnostics（编辑区）              |
| `tabstop`                         | snippet 占位符                                    |
