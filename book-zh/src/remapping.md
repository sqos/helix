## 键位重映射

Helix 目前支持通过简单的 TOML 配置文件进行单向键位重映射（未来可能会提供通过命令重绑定的更强大方案）。

键位映射可用于三类命令：

* **静态命令（Static commands）**：例如 `move_char_right`，通常用于移动和编辑。完整列表请参考 [Keymap](./keymap.html) 文档或源代码 [`helix-term/src/commands.rs`](https://github.com/helix-editor/helix/blob/master/helix-term/src/commands.rs) 中 `static_commands!` 宏调用。
* **可输入命令（Typable commands）**：可在命令模式（`:`）下执行的命令，例如 `:write!`。完整列表请参考 [Commands](./commands.md) 文档或源代码 [`helix-term/src/commands/typed.rs`](https://github.com/helix-editor/helix/blob/master/helix-term/src/commands/typed.rs) 中 `TypableCommandList`。
* **宏（Macros）**：按顺序执行的一系列键。宏以 `@` 开头并列出要执行的键，例如 `@miw` 可选中当前单词。宏键位序列中暂不支持嵌套宏。修饰键（如 Alt+o）可使用 `<A-o>` 表示，例如 `"@miw<A-o>"`。

### 配置示例

在配置目录下创建 `config.toml`（Linux 默认 `~/.config/helix`）：

> 💡 设置修饰键 + 按键时，使用 `C-X` 或 `A-X` 表示 Ctrl 或 Alt，组合 Shift 用 `-`，如 `C-S-esc`。宏中使用 `<C-X>` 或 `<A-X>` 区分普通键。

```toml
[keys.normal]
C-s = ":w"                        # Ctrl-s 保存文件
C-o = ":open ~/.config/helix/config.toml" # Ctrl-o 打开配置文件
a = "move_char_left"               # 'a' 移动光标左
w = "move_line_up"                 # 'w' 上移一行
"C-S-esc" = "extend_line"          # Ctrl-Shift-Esc 扩展行
g = { a = "code_action" }          # `ga` 执行代码动作
"ret" = ["open_below", "normal_mode"] # Enter 下方打开新行并返回普通模式
"A-x" = "@x<A-d>"                  # Alt-x 执行宏选择整行并删除

[keys.insert]
"A-x" = "normal_mode"     # Alt-x 进入普通模式
j = { k = "normal_mode" } # `jk` 退出插入模式
```

### 次要模式（Minor modes）

按下特定键可进入次要模式，绑定可通过嵌套定义：

```toml
[keys.insert.j]
k = "normal_mode"          # jk 退出插入模式

[keys.normal.g]
a = "code_action"          # ga 执行代码动作

[keys.normal.z]             # 在 view 模式下交换 j/k
j = "scroll_up"
k = "scroll_down"

[keys.normal."+"]           # 自定义次要模式绑定到 +
m = ":run-shell-command make"
c = ":run-shell-command cargo build"
t = ":run-shell-command cargo test"
```

### 特殊键和修饰键

Ctrl、Shift、Alt 分别用 `C-`、`S-`、`A-` 表示。

超级键（Windows/Linux Key 或 Mac Command）在支持增强键盘协议的终端中也可使用，前缀为 `Meta-`、`Cmd-` 或 `Win-`（互为同义）。

```toml
[keys.normal]
C-s = ":write"
Cmd-s = ":write"
```

常用特殊键：

| 键名           | 表示法           |
| ------------ | ------------- |
| Backspace    | `"backspace"` |
| Space        | `"space"`     |
| Return/Enter | `"ret"`       |
| Left         | `"left"`      |
| Right        | `"right"`     |
| Up           | `"up"`        |
| Down         | `"down"`      |
| Home         | `"home"`      |
| End          | `"end"`       |
| Page Up      | `"pageup"`    |
| Page Down    | `"pagedown"`  |
| Tab          | `"tab"`       |
| Delete       | `"del"`       |
| Insert       | `"ins"`       |
| Null         | `"null"`      |
| Escape       | `"esc"`       |
| <            | `"lt"`        |
| >            | `"gt"`        |

可通过 `no_op` 禁用某键，其他字符如 `?`、`!`、`-` 可直接使用：

```toml
[keys.normal]
"?" = ":write"
"!" = ":write"
"-" = ":write"
```

> ⚠️ 注意：`-` 不能与修饰键组合，例如 Alt + `-` 应写作 `A-minus`，`A--` 无效。
