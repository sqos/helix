## 语言设置

语言特定的配置以及语言服务器的设置在 `languages.toml` 文件中进行。

## `languages.toml` 文件

`languages.toml` 文件有三种可能的位置：

1. Helix 源代码中，位于 [Helix 仓库](https://github.com/helix-editor/helix/blob/master/languages.toml)。提供语言和语言服务器的默认配置。

2. 用户的 [配置目录](./configuration.md) 中，用于覆盖内置语言配置的值。例如，要禁用 Rust 的自动格式化：

```toml
# 位于 <config_dir>/helix/languages.toml

[language-server.mylang-lsp]
command = "mylang-lsp"

[[language]]
name = "rust"
auto-format = false
```

3. 项目中的 `.helix` 文件夹。可在项目本地通过创建 `languages.toml` 文件覆盖语言配置，其设置将与配置目录和内置配置合并。

## 语言配置

每种语言通过在 `languages.toml` 中添加 `[[language]]` 部分进行配置。例如：

```toml
[[language]]
name = "mylang"
scope = "source.mylang"
injection-regex = "mylang"
file-types = ["mylang", "myl"]
comment-tokens = "#"
indent = { tab-width = 2, unit = "  " }
formatter = { command = "mylang-formatter", args = ["--stdin"] }
language-servers = [ "mylang-lsp" ]
```

可用配置键：

| 键                               | 描述                                                                                                                                              |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`                          | 语言名称                                                                                                                                            |
| `language-id`                   | 语言服务器的语言 ID，参见 [TextDocumentItem](https://microsoft.github.io/language-server-protocol/specifications/lsp/3.17/specification/#textDocumentItem) |
| `scope`                         | 识别语言的字符串，如 `source.js`。通常使用 TextMate 语法和 Linguist 库的 scope 名称，标记语言使用 `text.<name>`                                                              |
| `injection-regex`               | 正则模式，用于判断是否在潜在的 [语言注入][treesitter-language-injection] 场景中使用该语言                                                                                  |
| `file-types`                    | 语言文件类型，例如 `["yml", "yaml"]`。参见下方文件类型检测说明                                                                                                        |
| `shebangs`                      | Shebang 行的解释器，例如 `["sh", "bash"]`                                                                                                               |
| `roots`                         | 寻找工作区根目录的标记文件，例如 `Cargo.lock`、`yarn.lock`                                                                                                       |
| `auto-format`                   | 保存时是否自动格式化该语言                                                                                                                                   |
| `diagnostic-severity`           | 显示诊断的最低严重等级，可选值：`error`、`warning`、`info`、`hint`                                                                                                 |
| `comment-tokens`                | 注释符号，单个字符串 `"//"` 或数组 `["//", "///", "//!"]`（首个用于注释）。向后兼容可使用 `comment-token`                                                                    |
| `block-comment-tokens`          | 多行注释的开始和结束符号，可为数组或单个表 `{ start = "/*", end = "*/" }`                                                                                            |
| `indent`                        | 缩进设置，子键 `unit`（缩进文本，通常为若干空格或 `"\t"`）和 `tab-width`（Tab 显示宽度）                                                                                     |
| `language-servers`              | 该语言使用的语言服务器，详见 [为语言配置语言服务器](#configuring-language-servers-for-a-language)                                                                       |
| `grammar`                       | 使用的 tree-sitter 语法，默认为 `name`                                                                                                                   |
| `formatter`                     | 语言格式化工具，优先于 LSP。必须能从 stdin 获取原始文件并写入 stdout，可使用 `%{buffer_name}` 传递当前缓冲文件名。详见 [配置格式化命令](#configuring-the-formatter-command)                     |
| `soft-wrap`                     | [editor.softwrap](./editor.md#editorsoft-wrap-section)                                                                                          |
| `text-width`                    | 最大行长度，用于 `:reflow` 命令和软换行（若 `soft-wrap.wrap-at-text-width` 启用），默认取 `editor.text-width`                                                          |
| `rulers`                        | 覆盖 `editor.rulers` 配置                                                                                                                           |
| `path-completion`               | 覆盖 `editor.path-completion` 配置                                                                                                                  |
| `word-completion`               | 覆盖 [`editor.word-completion`](./editor.md#editorword-completion-section) 配置                                                                     |
| `workspace-lsp-roots`           | 相对于工作区根目录的 LSP 根目录，仅在 `.helix/config.toml` 中设置时有效，会覆盖 `config.toml` 中同名设置                                                                       |
| `persistent-diagnostic-sources` | 假定未更改的 LSP 诊断源数组，当语言服务器重新发送相同诊断时，Helix 内部跟踪位置，适用于保存时重新计算的诊断                                                                                     |
| `rainbow-brackets`              | 覆盖语言的 `editor.rainbow-brackets` 配置                                                                                                              |

### 文件类型检测与 `file-types` 键

Helix 根据上述 `file-types` 键确定使用的语言配置。`file-types` 是字符串或表的列表，例如：

```toml
file-types = ["toml", { glob = "Makefile" }, { glob = ".git/config" }, { glob = ".github/workflows/*.yaml" }]
```

语言配置匹配优先级如下：

1. **Glob**：检查 `glob` 表的值是否匹配文件完整路径。支持标准 Unix 风格通配符（如 Shell 使用的通配符），可匹配特定前缀、后缀、目录等。例如：

   * `{ glob = "Makefile" }` 匹配文件名为 `Makefile`
   * `{ glob = ".git/config" }` 匹配 `.git` 目录下的 `config` 文件
   * `{ glob = ".github/workflows/*.yaml" }` 匹配 `.github/workflow` 下所有 `.yaml` 文件
     注意：Glob 始终使用 `/` 作为路径分隔符，Windows 系统自动适配机器特定分隔符；若 glob 不是绝对路径且未以通配符开头，会自动加上 `*/` 以匹配子目录。

2. **扩展名**：若没有 glob 匹配，使用文件扩展名匹配 `file-types` 字符串。例如 `"toml"` 匹配 `Cargo.toml` 或 `languages.toml` 文件。

### 配置格式化命令

格式化命令的参数支持 [命令行展开](./command-line.md#expansions)，特别是可以使用 `%{buffer_name}` 变量传递当前缓冲文件名：

```toml
formatter = { command = "mylang-formatter", args = ["--stdin", "--stdin-filename", "%{buffer_name}"] }
```

## 语言服务器配置

语言服务器在与语言相同的 `languages.toml` 文件中的 `language-server` 表中单独配置。

例如：

```toml
[language-server.mylang-lsp]
command = "mylang-lsp"
args = ["--stdio"]
config = { provideFormatter = true }
environment = { "ENV1" = "value1", "ENV2" = "value2" }

[language-server.efm-lsp-prettier]
command = "efm-langserver"

[language-server.efm-lsp-prettier.config]
documentFormatting = true
languages = { typescript = [ { formatCommand ="prettier --stdin-filepath ${INPUT}", formatStdin = true } ] }
```

可用配置选项：

| 键                        | 描述                                                            |
| ------------------------ | ------------------------------------------------------------- |
| `command`                | 要执行的语言服务器二进制文件名称或路径。必须在 `$PATH` 中                             |
| `args`                   | 传递给语言服务器二进制的参数列表                                              |
| `config`                 | 语言服务器初始化选项                                                    |
| `timeout`                | 请求语言服务器的最大时间（秒），默认 `20`                                       |
| `environment`            | 启动语言服务器时使用的环境变量，例如 `{ "KEY1" = "Value1", "KEY2" = "Value2" }` |
| `required-root-patterns` | 工作目录中要查找的 `glob` 模式列表。如果找到至少一个，则启动语言服务器                       |

在 `config` 中可使用 `format` 子表传递额外的格式化选项，用于 [文档格式化请求](https://microsoft.github.io/language-server-protocol/specifications/lsp/3.17/specification/#textDocument_formatting) 。例如 TypeScript：

```toml
[language-server.typescript-language-server]
# 根据 https://github.com/typescript-language-server/typescript-language-server#workspacedidchangeconfiguration 传递格式化选项，省略 "[language].format." 前缀。
config = { format = { "semicolons" = "insert", "insertSpaceBeforeFunctionParenthesis" = true } }
```

### 为语言配置语言服务器

语言中的 `language-servers` 属性指定 Helix 为该语言使用哪些语言服务器。

这些语言服务器必须在 `[language-server]` 表中定义，如上节所述。

不同语言可以使用同一语言服务器实例，例如 `typescript-language-server` 默认用于 javascript、jsx、tsx 和 typescript。

语言服务器的定义顺序会影响代码操作菜单的结果列表顺序。

如果在 `language-servers` 中指定多个语言服务器，通常需要为这些语言服务器启用/禁用某些功能。

例如，上节中的 `efm-lsp-prettier` 仅用于格式化命令 `prettier`，其他功能由默认配置的 `typescript-language-server` 处理。TypeScript 的语言配置可以如下：

```toml
[[language]]
name = "typescript"
language-servers = [ { name = "efm-lsp-prettier", only-features = [ "format" ] }, "typescript-language-server" ]
```

或等价配置：

```toml
[[language]]
name = "typescript"
language-servers = [ { name = "typescript-language-server", except-features = [ "format" ] }, "efm-lsp-prettier" ]
```

请求的 LSP 功能会按照 `language-servers` 数组的顺序优先处理。例如，第一个支持 `goto-definition` 的语言服务器（此处为 `typescript-language-server`）将用于相关 LSP 请求（命令 `goto_definition`）。
`diagnostics`、`code-action`、`completion`、`document-symbols` 和 `workspace-symbols` 是例外，这些功能可同时在所有启用的语言服务器中工作并合并。
若未指定 `except-features` 或 `only-features`，该语言服务器的所有功能均启用。若语言服务器不支持某功能，则尝试下一个语言服务器，依此类推。

支持的功能列表：

* `format`
* `goto-definition`
* `goto-declaration`
* `goto-type-definition`
* `goto-reference`
* `goto-implementation`
* `signature-help`
* `hover`
* `document-highlight`
* `completion`
* `code-action`
* `workspace-command`
* `document-symbols`
* `workspace-symbols`
* `diagnostics`
* `rename-symbol`
* `inlay-hints`

## Tree-sitter 语法配置

语言的 tree-sitter 语法源在 `languages.toml` 的 `[[grammar]]` 部分指定。例如：

```toml
[[grammar]]
name = "mylang"
source = { git = "https://github.com/example/mylang", rev = "a250c4582510ff34767ec3b7dcdd3c24e8c8aa68" }
```

语法配置包含以下键：

| 键        | 描述                           |
| -------- | ---------------------------- |
| `name`   | tree-sitter 语法的名称            |
| `source` | 获取语法的方法 —— 一个包含下述 schema 的表格 |

当 `source` 使用来自 git 仓库的语法时，可包含以下键：

| 键         | 描述                                                                                                                                 |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `git`     | 要克隆语法的 git 远程 URL                                                                                                                  |
| `rev`     | 要获取的版本（提交哈希或标签）                                                                                                                    |
| `subpath` | 语法目录中用于构建的子路径。一些语法仓库在子目录中托管多个语法（例如 `tree-sitter-typescript` 和 `tree-sitter-ocaml`）。此键用于指向 `hx --grammar build` 构建正确路径。若省略，则使用仓库根目录 |

### 选择语法

可以使用顶级 `use-grammars` 键来控制在执行 `hx --grammar fetch` 和 `hx --grammar build` 时获取和构建哪些语法。

```toml
# 注意：该键必须放在 [[language]] 和 [[grammar]] 部分之前
use-grammars = { only = [ "rust", "c", "cpp" ] }
# 或者
use-grammars = { except = [ "yaml", "json" ] }
```

若省略，则会获取并构建所有语法。

[treesitter-language-injection]: https://tree-sitter.github.io/tree-sitter/3-syntax-highlighting.html#language-injection

