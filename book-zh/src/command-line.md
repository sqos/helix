# 命令行

* [引用](#quoting)
* [标志](#flags)
* [扩展](#expansions)
* [例外](#exceptions)

命令行用于执行像 `:write` 或 `:quit` 这样的[可输入命令](./commands.md#typable-commands)。按 `:` 激活命令行。

可输入命令可以选择性地接受参数。例如 `:write` 可以接受一个可选路径以写入文件内容。命令行还支持参数的引用语法、用于修改命令行为的标志，以及**扩展** —— 一种从编辑器插入值的方式。大多数命令支持这些功能，但部分命令有自定义解析规则（见下文[例外](#exceptions)）。

## 引用

默认情况下，命令参数以制表符和空格分隔。例如 `:open README.md CHANGELOG.md` 应该打开两个文件 `README.md` 和 `CHANGELOG.md`。包含空格的参数可以用单引号（`'`）或反引号（`` ` ``）包裹，以防空格分隔参数，例如 `:open 'a b.txt'`。

双引号可以以同样方式使用，但双引号会**展开**其内部内容。例如 `:echo "%{cursor_line}"` 可能打印 `1`，因为 `cursor_line` 变量被展开。而 `:echo '%{cursor_line}'` 则会原样打印 `%{cursor_line}`：单引号或反引号内的内容按原样解释。

在 Unix 系统中，反斜杠字符（`\`）可用于对某些字符进行转义，其具体行为取决于使用位置。在未用引号包围的参数中，反斜杠可以用来转义空格或制表符：例如，`:open a\ b.txt` 等价于 `:open 'a b.txt'`。反斜杠也可以用于转义引号字符（`'`、`` ` ``、`"`）或百分号标记（`%`），但仅在参数开头时有效。例如，`:echo \%sh{foo}` 会打印 `%sh{foo}`，而不会执行 `foo` 作为 Shell 命令；`:echo \"quote` 则打印 `"quote`。在 Unix 系统中，其他情况下反斜杠被视为字面字符；在 Windows 系统中则始终如此。例如，`:echo \n` 总是输出 `\n`，而不会被解释为换行符。

## 标志

命令标志是可选开关，可用于修改命令行为。例如 `:sort` 命令接受可选标志 `--reverse`（或简写 `-r`），用于反转排序方向。输入 `-` 字符可以显示当前命令的标志补全（如果有的话）。

`--` 标志表示标志结束。`--` 后的所有参数都被视为位置参数：`:open -- -a.txt` 会打开名为 `-a.txt` 的文件。

## 扩展

扩展是 Helix 在命令行中识别并替换的模式。Helix 将任何以百分号 (`%`) 开头的内容视为扩展，例如 `%sh{echo hi!}`。扩展在像 `:echo` 或 `:noop` 这样的命令中尤其有用，用于执行简单脚本。例如：

```toml
[keys.normal]
# 在状态栏打印当前行的 git blame 信息
space.B = ":echo %sh{git blame -L %{cursor_line},+1 %{buffer_name}}"
```

扩展形式为 `%[<kind>]<open><contents><close>`。例如 `%sh{echo hi!}` 中，kind 是 `sh`（shell 扩展），内容是 `echo hi!`，`{` 和 `}` 是开闭分隔符。支持的分隔符对包括：`(`/`)`、`[`/`]`、`{`/`}` 和 `<`/`>`。单字符 `'`、`"` 或 `|` 也可用作分隔符：`%{cursor_line}` 等价于 `%<cursor_line>`、`%[cursor_line]` 或 `%|cursor_line|`。

要转义百分号而不作为扩展使用，可连续使用两个百分号。要执行像 `date -u +'%Y-%m-%d'` 的 shell 命令，可双写百分号：`:echo %sh{date -u +'%%Y-%%m-%%d'}`。

当未提供 `<kind>` 时，Helix 会展开为**变量**。例如 `%{cursor_line}` 可用作参数插入行号。`:echo %{cursor_line}` 可能在状态栏打印 `1`。

支持的变量如下：

| 名称                          | 描述                                                                                                    |
| --------------------------- | ----------------------------------------------------------------------------------------------------- |
| `cursor_line`               | 当前聚焦文档中主光标的行号，从 1 开始。                                                                                 |
| `cursor_column`             | 当前聚焦文档中主光标的列号，从 1 开始。按从行首算起的**字符群集数**而非字节或代码点计数。                                                      |
| `buffer_name`               | 当前聚焦文档的相对路径。对于临时缓冲区，展开为 `[scratch]`。                                                                  |
| `line_ending`               | 当前聚焦文档的行结束符字符串。例如在 Unix 系统通常为换行符 (`\n`)，在 Windows 系统可能为回车+换行 (`\r\n`)。可用 `:line-ending` 查看当前文档的行结束类型。 |
| `current_working_directory` | 当前工作目录                                                                                                |
| `workspace_directory`       | 包含 `.git`、`.svn`、`jj` 或 `.helix` 的当前工作目录的最近祖先目录                                                       |
| `language`                  | 当前聚焦文档的语言名称字符串                                                                                        |
| `selection`                 | 当前聚焦文档主选区的内容字符串                                                                                       |
| `selection_line_start`      | 当前聚焦文档主选区开始行号，从 1 开始                                                                                  |
| `selection_line_end`        | 当前聚焦文档主选区结束行号，从 1 开始                                                                                  |

除了编辑器变量，还可使用以下扩展：

* Unicode `%u{..}`：内容可包含最多六位十六进制数，对应 Unicode 码点。例如 `:echo %u{25CF}` 打印 `●`。
* Shell `%sh{..}`：内容传给配置的 shell 命令。例如 `:echo %sh{echo "20 * 5" | bc}` 若系统安装了 `echo` 和 `bc`，状态栏可能打印 `100`。Shell 扩展会递归求值。例如 `%sh{echo '%{buffer_name}:%{cursor_line}'}` 会执行类似 `echo 'README.md:1'` 的命令：扩展中的变量先被求值，然后执行 shell 命令。

如前所述，双引号可包裹带空格的参数，并支持内部扩展，而单引号或反引号不支持。例如 `:echo "circle: %u{25CF}"` 打印 `circle: ●`，而 `:echo 'circle: %u{25CF}'` 打印 `circle: %u{25CF}`。

注意，扩展仅在命令模式按下 Enter 键后求值。

## 例外

以下命令支持扩展，但会将给定参数直接传递给 shell，而不解析引号：

* `:insert-output`
* `:append-output`
* `:pipe`
* `:pipe-to`
* `:run-shell-command`

例如执行 `:sh echo "%{buffer_name}:%{cursor_column}"` 会将文本 `echo "README.md:1"` 作为参数传给 shell：扩展被求值，但引号不被解析。如前所述，百分号可通过双写在 shell 命令中使用。要插入像 `date -u +'%Y-%m-%d'` 的命令输出，可用 `:insert-output date -u +'%%Y-%%m-%%d'`。

`:set-option` 和 `:toggle-option` 命令对第一个参数（配置选项名）使用普通解析，其余参数根据配置选项类型解析。`:set-option` 将第二个参数作为字符串解析（字符串类型配置），其他解析为 JSON。

`:toggle-option` 行为取决于第一个参数提供的配置选项的 JSON 类型：

* 布尔值：只提供配置选项名。例如 `:toggle-option auto-format` 会切换 `auto-format`。
* 字符串：命令行剩余部分按常规引用规则解析。例如 `:toggle-option indent-heuristic hybrid tree-sitter simple` 每次调用依次循环 "hybrid"、"tree-sitter" 和 "simple"。
* 数字、数组和对象：命令行剩余部分作为 JSON 值流解析。例如 `:toggle-option rulers [81] [51, 73]` 循环 `[81]` 和 `[51, 73]`。

提供多个值时不应有重复。例如 `:toggle-option indent-heuristic hybrid simple tree-sitter simple` 仅在 "hybrid" 与 "tree-sitter" 之间切换。

`:lsp-workspace-command` 与 `:toggle-option` 类似。第一个参数（如果存在）按普通规则解析，其余命令行作为 JSON 值解析。不同于 `:toggle-option`，命令的字符串参数必须加引号。例如 `:lsp-workspace-command lsp.Command "foo" "bar"`。
