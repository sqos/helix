## Editor

- [Editor](#editor)
  - [`[editor]` Section](#editor-section)
  - [`[editor.clipboard-provider]` Section](#editorclipboard-provider-section)
  - [`[editor.statusline]` Section](#editorstatusline-section)
  - [`[editor.lsp]` 部分](#editorlsp-部分)
  - [`[editor.cursor-shape]` Section](#editorcursor-shape-section)
  - [`[editor.file-picker]` 部分](#editorfile-picker-部分)
  - [`[editor.file-explorer]` Section](#editorfile-explorer-section)
  - [`[editor.auto-pairs]` 部分](#editorauto-pairs-部分)
  - [`[editor.auto-save]` 部分](#editorauto-save-部分)
  - [`[editor.search]` 部分](#editorsearch-部分)
  - [`[editor.whitespace]` 部分](#editorwhitespace-部分)
  - [`[editor.indent-guides]` Section](#editorindent-guides-section)
  - [`[editor.gutters]` 部分](#editorgutters-部分)
    - [`[editor.gutters.line-numbers]` 部分](#editorguttersline-numbers-部分)
    - [`[editor.gutters.diagnostics]` 部分](#editorguttersdiagnostics-部分)
    - [`[editor.gutters.diff]` 部分](#editorguttersdiff-部分)
    - [`[editor.gutters.spacer]` 部分](#editorguttersspacer-部分)
  - [`[editor.soft-wrap]` 部分](#editorsoft-wrap-部分)
  - [`[editor.smart-tab]` 部分](#editorsmart-tab-部分)
  - [`[editor.inline-diagnostics]` 部分](#editorinline-diagnostics-部分)
  - [`[editor.word-completion]` 部分](#editorword-completion-部分)

### `[editor]` Section

| 键（Key）                      | 描述（Description）                                                                                                            | 默认值（Default）                                                  |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| `scrolloff`                 | 滚动时屏幕边缘周围的行数填充                                                                                                             | `5`                                                           |
| `mouse`                     | 启用鼠标模式                                                                                                                     | `true`                                                        |
| `default-yank-register`     | 默认用于复制/粘贴的寄存器                                                                                                              | `'"'`                                                         |
| `middle-click-paste`        | 支持鼠标中键粘贴                                                                                                                   | `true`                                                        |
| `scroll-lines`              | 每次滚轮滚动的行数                                                                                                                  | `3`                                                           |
| `shell`                     | 运行外部命令时使用的 shell                                                                                                           | Unix: `["sh", "-c"]`<br/>Windows: `["cmd", "/C"]`             |
| `line-number`               | 行号显示：`absolute` 显示绝对行号，`relative` 显示相对于当前行的距离。在非焦点或插入模式下，`relative` 仍显示绝对行号                                                | `"absolute"`                                                  |
| `cursorline`                | 高亮光标所在的整行                                                                                                                  | `false`                                                       |
| `cursorcolumn`              | 高亮光标所在的整列                                                                                                                  | `false`                                                       |
| `continue-comments`         | 在注释内部创建新行时自动添加行注释符                                                                                                         | `true`                                                        |
| `gutters`                   | 显示边栏：可用选项包括 `diagnostics`、`diff`、`line-numbers` 和 `spacer`。如果非空，`diagnostics` 也会包括其他功能，并插入 1 宽度的填充                         | `["diagnostics", "spacer", "line-numbers", "spacer", "diff"]` |
| `auto-completion`           | 启用自动补全弹出                                                                                                                   | `true`                                                        |
| `path-completion`           | 启用路径补全。如果光标处识别到路径（绝对或相对当前文件或工作目录），显示文件和目录                                                                                  | `true`                                                        |
| `auto-format`               | 保存时自动格式化                                                                                                                   | `true`                                                        |
| `idle-timeout`              | 从上次按键起触发空闲定时器的毫秒数                                                                                                          | `250`                                                         |
| `completion-timeout`        | 输入单词字符后等待多长时间显示补全，设为 5 可立即触发                                                                                               | `250`                                                         |
| `preview-completion-insert` | 是否在选中补全项时立即应用                                                                                                              | `true`                                                        |
| `completion-trigger-len`    | 触发自动补全的最小单词长度                                                                                                              | `2`                                                           |
| `completion-replace`        | 是否总是替换整个单词，而不仅替换光标前的部分                                                                                                     | `false`                                                       |
| `auto-info`                 | 是否显示信息框                                                                                                                    | `true`                                                        |
| `true-color`                | 是否覆盖终端真彩色支持的自动检测（用于检测为假负时）                                                                                                 | `false`                                                       |
| `undercurl`                 | 是否覆盖终端下划波浪线支持的自动检测（用于检测为假负时）                                                                                               | `false`                                                       |
| `rulers`                    | 显示标尺的列位置列表，可被 `languages.toml` 中语言特定设置覆盖                                                                                   | `[]`                                                          |
| `bufferline`                | 顶部显示打开缓冲区的行，可选值 `always`、`never` 或 `multiple`（仅当打开多个缓冲区时显示）                                                                | `"never"`                                                     |
| `color-modes`               | 是否根据模式改变模式指示器颜色                                                                                                            | `false`                                                       |
| `text-width`                | 最大行长度，用于 `:reflow` 命令及软换行（当 `soft-wrap.wrap-at-text-width` 启用时）                                                            | `80`                                                          |
| `workspace-lsp-roots`       | 相对于工作区根目录的 LSP 根目录列表，仅在 `.helix/config.toml` 中设置                                                                           | `[]`                                                          |
| `default-line-ending`       | 新建文档的行结束符，可选：`native`、`lf`、`crlf`、`ff`、`cr`、`nel`。`native` 使用平台默认（Windows 为 `crlf`，其他为 `lf`）                               | `"native"`                                                    |
| `insert-final-newline`      | 写入时自动在末尾添加行结束符（如缺失）                                                                                                        | `true`                                                        |
| `atomic-save`               | 是否使用原子操作写入文件，防止编辑器中断导致数据丢失，但可能影响文件监控/热重载                                                                                   | `true`                                                        |
| `trim-final-newlines`       | 写入时自动删除末尾多余行结束符                                                                                                            | `false`                                                       |
| `trim-trailing-whitespace`  | 写入时自动删除行尾空白                                                                                                                | `false`                                                       |
| `popup-border`              | 弹出框边框：`popup`、`menu`、`all` 或 `none`                                                                                        | `"none"`                                                      |
| `indent-heuristic`          | 新行缩进策略：`simple` 复制上一行缩进，`tree-sitter` 根据语法树计算，`hybrid` 混合两者。如选定策略不可用，按顺序使用 fallback（`hybrid` -> `tree-sitter` -> `simple`） | `"hybrid"`                                                    |
| `jump-label-alphabet`       | 用于生成两字符跳转标签的字符集合，优先使用前面的字符                                                                                                 | `"abcdefghijklmnopqrstuvwxyz"`                                |
| `end-of-line-diagnostics`   | 行尾显示诊断的最小严重等级，设置为 `disable` 可完全禁用                                                                                          | `"hint"`                                                      |
| `clipboard-provider`        | 剪贴板接口，可选：`pasteboard` (MacOS)、`wayland`、`x-clip`、`x-sel`、`win32-yank`、`termux`、`tmux`、`windows`、`termcode`、`none` 或自定义命令   | 平台和环境相关                                                       |
| `editor-config`             | 是否读取 [EditorConfig](https://editorconfig.org) 配置文件                                                                         | `true`                                                        |
| `rainbow-brackets`          | 是否启用括号彩虹渲染，需要 tree-sitter `rainbows.scm` 查询文件支持                                                                            | `false`                                                       |
| `kitty-keyboard-protocol`   | 是否启用 Kitty 键盘协议，可选 `enabled`、`disabled` 或 `auto`                                                                           | `"auto"`                                                      |

### `[editor.clipboard-provider]` Section

Helix 可以配置为使用内置剪贴板，或者使用提供的自定义命令。

例如，将其设置为使用 OSC 52 Termcodes，配置如下：

```toml
[editor]
clipboard-provider = "termcode"
```

或者，Helix 也可以配置为使用任意命令进行剪贴板集成：

```toml
[editor.clipboard-provider.custom]
yank = { command = "cat",  args = ["test.txt"] }
paste = { command = "tee",  args = ["test.txt"] }
primary-yank = { command = "cat",  args = ["test-primary.txt"] } # 可选
primary-paste = { command = "tee",  args = ["test-primary.txt"] } # 可选
```

对于自定义命令，yank/paste 的内容通过 stdin/stdout 进行传输。

### `[editor.statusline]` Section

允许配置编辑器底部的状态栏。

配置将状态栏分为三个区域：

`[ ... ... LEFT ... ... | ... ... ... CENTER ... ... ... | ... ... RIGHT ... ... ]`

状态栏元素可以如下定义：

```toml
[editor.statusline]
left = ["mode", "spinner"]
center = ["file-name"]
right = ["diagnostics", "selections", "position", "file-encoding", "file-line-ending", "file-type"]
separator = "│"
mode.normal = "NORMAL"
mode.insert = "INSERT"
mode.select = "SELECT"
diagnostics = ["warning", "error"]
workspace-diagnostics = ["warning", "error"]
```

`[editor.statusline]` 键包含以下子键：

| 键                       | 描述                        | 默认值                                                                                      |
| ----------------------- | ------------------------- | ---------------------------------------------------------------------------------------- |
| `left`                  | 对齐到状态栏左侧的元素列表             | `["mode", "spinner", "file-name", "read-only-indicator", "file-modification-indicator"]` |
| `center`                | 对齐到状态栏中间的元素列表             | `[]`                                                                                     |
| `right`                 | 对齐到状态栏右侧的元素列表             | `["diagnostics", "selections", "register", "position", "file-encoding"]`                 |
| `separator`             | 用于分隔状态栏元素的字符              | `"│"`                                                                                    |
| `mode.normal`           | normal 模式下 `mode` 元素显示的文本 | `"NOR"`                                                                                  |
| `mode.insert`           | insert 模式下 `mode` 元素显示的文本 | `"INS"`                                                                                  |
| `mode.select`           | select 模式下 `mode` 元素显示的文本 | `"SEL"`                                                                                  |
| `diagnostics`           | 当前缓冲区显示的诊断等级列表            | `["warning", "error"]`                                                                   |
| `workspace-diagnostics` | 工作区显示的诊断等级列表              | `["warning", "error"]`                                                                   |

以下状态栏元素可以配置：

| 键                             | 描述                                                  |
| ----------------------------- | --------------------------------------------------- |
| `mode`                        | 当前编辑器模式 (`mode.normal`/`mode.insert`/`mode.select`) |
| `spinner`                     | 显示 LSP 活动的进度旋转器                                     |
| `file-name`                   | 打开的文件路径/名称                                          |
| `file-absolute-path`          | 打开的文件绝对路径/名称                                        |
| `file-base-name`              | 打开的文件的基础名称                                          |
| `current-working-directory`   | 当前工作目录                                              |
| `file-modification-indicator` | 指示文件是否已修改（有未保存更改时显示 `[+]`）                          |
| `file-encoding`               | 打开文件的编码（如果不是 UTF-8）                                 |
| `file-line-ending`            | 文件行结束符（CRLF 或 LF）                                   |
| `file-indent-style`           | 文件缩进风格                                              |
| `read-only-indicator`         | 当文件不可写时显示 `[readonly]` 指示符                          |
| `total-line-numbers`          | 打开文件的总行数                                            |
| `file-type`                   | 打开文件的类型                                             |
| `diagnostics`                 | 警告和/或错误数量                                           |
| `workspace-diagnostics`       | 工作区的警告和/或错误数量                                       |
| `selections`                  | 主选区在活动选区中的索引                                        |
| `primary-selection-length`    | 当前主选区中的字符数                                          |
| `position`                    | 光标位置                                                |
| `position-percentage`         | 光标位置占总行数的百分比                                        |
| `separator`                   | 由 `editor.statusline.separator` 定义的字符串（默认为 `"│"`）   |
| `spacer`                      | 在元素之间插入空格（可指定多个连续空格）                                |
| `version-control`             | 打开工作区的当前分支名或分离的提交哈希                                 |
| `register`                    | 当前选中的寄存器                                            |

---

### `[editor.lsp]` 部分

| 键                                    | 描述                                                        | 默认值     |
| ------------------------------------ | --------------------------------------------------------- | ------- |
| `enable`                             | 启用 LSP 集成。设置为 false 将完全禁用语言服务器，无论语言设置如何。                  | `true`  |
| `display-messages`                   | 在状态栏下方显示 LSP `window/showMessage` 消息[^1]                  | `true`  |
| `display-progress-messages`          | 在状态栏下方显示 LSP 进度消息[^1]                                     | `false` |
| `auto-signature-help`                | 启用自动弹出函数签名帮助（参数提示）                                        | `true`  |
| `display-inlay-hints`                | 显示内联提示[^2]                                                | `false` |
| `inlay-hints-length-limit`           | 内联提示显示的最大长度（非零数值）                                         | 默认未设置   |
| `display-color-swatches`             | 在颜色旁显示颜色样本                                                | `true`  |
| `display-signature-help-docs`        | 在签名帮助弹窗下显示文档                                              | `true`  |
| `snippets`                           | 启用代码片段补全。在 `:config-reload`/`:set` 后需要 `:lsp-restart` 才生效 | `true`  |
| `goto-reference-include-declaration` | 在跳转引用弹窗中包含声明                                              | `true`  |

[^1]: 默认情况下，状态栏在文件路径旁显示进度旋转器。

[^2]: 你可能还需要在语言服务器配置中启用内联提示，Helix 中的内联提示仍在改进中，在某些情况下可能略有延迟或不稳定。如发现任何问题，请反馈以便修复。

### `[editor.cursor-shape]` Section

定义各模式下光标的形状。
有效值为 `block`、`bar`、`underline` 或 `hidden`。

> 💡 由于终端环境的限制，只有主光标可以更改形状。

| 键        | 描述                         | 默认值       |
| -------- | -------------------------- | --------- |
| `normal` | [普通模式][normal mode] 下的光标形状 | `"block"` |
| `insert` | [插入模式][insert mode] 下的光标形状 | `"block"` |
| `select` | [选择模式][select mode] 下的光标形状 | `"block"` |

[normal mode]: ./keymap.md#normal-mode
[insert mode]: ./keymap.md#insert-mode
[select mode]: ./keymap.md#select--extend-mode

---

### `[editor.file-picker]` 部分

设置文件选择器和全局搜索的选项。被忽略的文件在 Helix 文件选择器和全局搜索中不可见。

所有与 Git 相关的选项仅在 Git 仓库中启用。

| 键                   | 描述                                                         | 默认值    |
| ------------------- | ---------------------------------------------------------- | ------ |
| `hidden`            | 启用忽略隐藏文件                                                   | `true` |
| `follow-symlinks`   | 跟随符号链接而不是忽略它们                                              | `true` |
| `deduplicate-links` | 忽略指向已在选择器中显示文件的符号链接                                        | `true` |
| `parents`           | 启用从父目录读取忽略文件                                               | `true` |
| `ignore`            | 启用读取 `.ignore` 文件                                          | `true` |
| `git-ignore`        | 启用读取 `.gitignore` 文件                                       | `true` |
| `git-global`        | 启用读取全局 `.gitignore` 文件，路径由 Git 配置中的 `core.excludesfile` 指定 | `true` |
| `git-exclude`       | 启用读取 `.git/info/exclude` 文件                                | `true` |
| `max-depth`         | 设置递归的最大深度（整数值）                                             | 默认未设置  |

忽略文件可以放在本地作为 `.ignore`，或放在用户主目录下为 `~/.ignore`。它们支持 `.gitignore` 文件中常用的忽略和取消忽略规则。

此外，你还可以使用 Helix 特有的忽略文件：

* 在当前工作区创建本地 `.helix/ignore`
* 在 Helix 配置目录创建全局 `ignore` 文件：

  * Linux 和 Mac: `~/.config/helix/ignore`
  * Windows: `%AppData%\helix\ignore`

示例：

```ini
# 在文件选择器和全局搜索中取消忽略
!.github/
!.gitignore
!.gitattributes
```

### `[editor.file-explorer]` Section

除了文件选择器和全局搜索的选项外，还提供了一组类似的选项用于单独配置文件资源管理器。然而，与文件选择器不同，默认设置避免忽略大多数文件。

注意，当 `ignore` 设置为 true 时，文件资源管理器使用的忽略文件与文件选择器相同，包括前面提到的 Helix 特有忽略文件。

| 键                 | 描述                                                         | 默认值     |
| ----------------- | ---------------------------------------------------------- | ------- |
| `hidden`          | 启用忽略隐藏文件                                                   | `false` |
| `follow-symlinks` | 跟随符号链接而不是忽略它们                                              | `false` |
| `parents`         | 启用从父目录读取忽略文件                                               | `false` |
| `ignore`          | 启用读取 `.ignore` 文件                                          | `false` |
| `git-ignore`      | 启用读取 `.gitignore` 文件                                       | `false` |
| `git-global`      | 启用读取全局 `.gitignore` 文件，路径由 Git 配置中的 `core.excludesfile` 指定 | `false` |
| `git-exclude`     | 启用读取 `.git/info/exclude` 文件                                | `false` |
| `flatten-dirs`    | 启用将单子目录展开                                                  | `true`  |

---

### `[editor.auto-pairs]` 部分

启用对括号、方括号等的自动配对插入。可以是简单的布尔值，也可以是单字符配对的具体映射。

要完全禁用自动配对，将 `auto-pairs` 设置为 `false`：

```toml
[editor]
auto-pairs = false # 默认为 `true`
```

默认配对为 <code>(){}[]''""``</code>，但可以通过将 `auto-pairs` 设置为 TOML 表进行自定义：

```toml
[editor.auto-pairs]
'(' = ')'
'{' = '}'
'[' = ']'
'"' = '"'
'`' = '`'
'<' = '>'
```

此外，此设置可用于语言配置中。除非编辑器设置为 `false`，否则在该语言文档中会覆盖编辑器配置。

示例 `languages.toml`，添加 `<>` 并移除 `''`：

```toml
[[language]]
name = "rust"

[language.auto-pairs]
'(' = ')'
'{' = '}'
'[' = ']'
'"' = '"'
'`' = '`'
'<' = '>'
```

---

### `[editor.auto-save]` 部分

控制自动保存行为。

| 键                     | 描述                                                                                                  | 默认值     |
| --------------------- | --------------------------------------------------------------------------------------------------- | ------- |
| `focus-lost`          | 在 Helix 失去焦点时自动保存。需要终端支持 [focus event](https://github.com/helix-editor/helix/wiki/Terminal-Support) | `false` |
| `after-delay.enable`  | 在距上次编辑指定毫秒后自动保存                                                                                     | `false` |
| `after-delay.timeout` | 距上次编辑多长时间（毫秒）触发自动保存计时器                                                                              | `3000`  |

---

### `[editor.search]` 部分

搜索相关选项。

| 键             | 描述                           | 默认值    |
| ------------- | ---------------------------- | ------ |
| `smart-case`  | 启用智能大小写正则搜索（模式中无大写字符时不区分大小写） | `true` |
| `wrap-around` | 搜索匹配用尽后是否从头开始循环              | `true` |

---

### `[editor.whitespace]` 部分

用于可视化空白字符的渲染。使用 `:set whitespace.render all` 可临时启用可见空白。

| 键            | 描述                                                                               | 默认值      |
| ------------ | -------------------------------------------------------------------------------- | -------- |
| `render`     | 是否渲染空白字符。可以是 `all` 或 `none`，也可以是包含子键 `space`、`nbsp`、`nnbsp`、`tab` 和 `newline` 的表 | `"none"` |
| `characters` | 渲染空白字符时使用的字符。子键可以是 `tab`、`space`、`nbsp`、`nnbsp`、`newline` 或 `tabpad`             | 见示例      |

例如

```toml
[editor.whitespace]
render = "all"
# or control each character
[editor.whitespace.render]
space = "all"
tab = "all"
nbsp = "none"
nnbsp = "none"
newline = "none"

[editor.whitespace.characters]
space = "·"
nbsp = "⍽"
nnbsp = "␣"
tab = "→"
newline = "⏎"
tabpad = "·" # Tabs will look like "→···" (depending on tab width)
```

### `[editor.indent-guides]` Section

垂直缩进指示线渲染选项：

| 键             | 描述           | 默认值     |
| ------------- | ------------ | ------- |
| `render`      | 是否渲染缩进指示线    | `false` |
| `character`   | 用于渲染缩进指示线的字符 | `"│"`   |
| `skip-levels` | 跳过的缩进级别数     | `0`     |

示例：

```toml
[editor.indent-guides]
render = true
character = "╎" # 可用字符示例: "▏", "┆", "┊", "⸽"
skip-levels = 1
```

---

### `[editor.gutters]` 部分

为简便起见，`editor.gutters` 接受一个 gutter 类型数组，使用所有 gutter 组件的默认设置。

```toml
[editor]
gutters = ["diff", "diagnostics", "line-numbers", "spacer"]
```

要自定义 gutter 行为，需要使用 `[editor.gutters]` 部分。该部分包含顶层设置以及特定 gutter 组件的子设置。

| 键        | 描述               | 默认值                                                           |
| -------- | ---------------- | ------------------------------------------------------------- |
| `layout` | 要显示的 gutter 顺序数组 | `["diagnostics", "spacer", "line-numbers", "spacer", "diff"]` |

示例：

```toml
[editor.gutters]
layout = ["diff", "diagnostics", "line-numbers", "spacer"]
```

#### `[editor.gutters.line-numbers]` 部分

行号 gutter 选项：

| 键           | 描述       | 默认值 |
| ----------- | -------- | --- |
| `min-width` | 使用的最少字符数 | `3` |

示例：

```toml
[editor.gutters.line-numbers]
min-width = 1
```

#### `[editor.gutters.diagnostics]` 部分

当前未使用。

#### `[editor.gutters.diff]` 部分

`diff` gutter 显示彩色条，表示 Git diff 中某行是新增、删除还是修改。颜色由主题属性 `diff.plus`、`diff.minus` 和 `diff.delta` 控制。

未来插件系统可能支持其他 diff 提供者。

当前此部分没有额外选项。

#### `[editor.gutters.spacer]` 部分

当前未使用。

---

### `[editor.soft-wrap]` 部分

超出视图宽度的行软换行选项：

| 键                    | 描述                                 | 默认值     |
| -------------------- | ---------------------------------- | ------- |
| `enable`             | 是否启用软换行                            | `false` |
| `max-wrap`           | 行末保留的最大空白                          | `20`    |
| `max-indent-retain`  | 软换行时保留的最大缩进                        | `40`    |
| `wrap-indicator`     | 插入在软换行行前的文本，高亮使用 `ui.virtual.wrap` | `"↪ "`  |
| `wrap-at-text-width` | 是否在 `text-width` 处软换行，而非使用整个视口宽度   | `false` |

示例：

```toml
[editor.soft-wrap]
enable = true
max-wrap = 25
max-indent-retain = 0
wrap-indicator = ""  # 隐藏 wrap 指示符
```

---

### `[editor.smart-tab]` 部分

使用 Tab 键进行导航和编辑的选项。

| 键                | 描述                                                                                          | 默认值     |
| ---------------- | ------------------------------------------------------------------------------------------- | ------- |
| `enable`         | 若光标左侧有非空白字符，则执行 `move_parent_node_end`；若仅有空白，则插入 Tab。默认绑定下，显式插入 Tab 请使用 Shift-tab。          | `true`  |
| `supersede-menu` | 当菜单显示（如自动完成触发时），Tab 通常用于循环菜单项。若启用此选项，`smart-tab` 命令优先，Tab 无法循环菜单项，需使用其他绑定如箭头键或 `C-n`/`C-p`。 | `false` |

部分终端不支持 S-tab，默认按键绑定无法完全体验 smart-tab。若终端支持 [Enhanced Keyboard protocol](https://github.com/helix-editor/helix/wiki/Terminal-Support#enhanced-keyboard-protocol)，可设置额外按键绑定：

```
[keys.normal]
tab = "move_parent_node_end"
S-tab = "move_parent_node_start"

[keys.insert]
S-tab = "move_parent_node_start"

[keys.select]
tab = "extend_parent_node_end"
S-tab = "extend_parent_node_start"
```

---

### `[editor.inline-diagnostics]` 部分

在文本中显示诊断信息，例如：

```
fn main() {
  let foo = bar;
            └─ no such value in this scope
}
```

| 键                 | 描述                                                             | 默认值         |
| ----------------- | -------------------------------------------------------------- | ----------- |
| `cursor-line`     | 光标所在行显示的诊断最低等级。设置为 `disable` 禁用该行内联诊断。在插入模式下无效，光标移动 350ms 后生效。 | `"warning"` |
| `other-lines`     | 非光标行显示的诊断最低等级。设置为 `disable` 禁用该行内联诊断。                          | `"disable"` |
| `prefix-len`      | 诊断文本前渲染的水平条 `─` 数量                                             | `1`         |
| `max-wrap`        | 诊断信息软换行最大宽度（同 `editor.soft-wrap.max-wrap`）                     | `20`        |
| `max-diagnostics` | 每行最大渲染诊断数量                                                     | `10`        |

`cursor-line` 和 `other-lines` 可选值：`error`、`warning`、`info`、`hint`。

未在行内显示的最高严重等级诊断会显示在行尾（若其严重等级高于 `end-of-line-diagnostics` 配置）：

```
fn main() {
  let baz = 1;
  let foo = bar; a local variable with a similar name exists: baz
            └─ no such value in this scope
}
```

---

### `[editor.word-completion]` 部分

控制从打开缓冲区完成单词的选项：

| 键                | 描述             | 默认值    |
| ---------------- | -------------- | ------ |
| `enable`         | 是否启用单词补全       | `true` |
| `trigger-length` | 触发补全前需输入的单词字符数 | `7`    |

示例：

```toml
[editor.word-completion]
enable = true
# 将触发长度设置更低，以更频繁补全单词
trigger-length = 4
```
