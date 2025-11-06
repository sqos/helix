## 命令参考（Commands）

| 命令                                                | 说明                                                          |
| ------------------------------------------------- | ----------------------------------------------------------- |
| `:exit`, `:x`, `:xit`                             | 如果缓冲区已修改，则写入磁盘后退出。可带可选路径参数（`:exit some/path.txt`）。          |
| `:exit!`, `:x!`, `:xit!`                          | 强制写入修改到磁盘，必要时创建子目录，然后退出。可带可选路径参数（`:exit! some/path.txt`）。   |
| `:quit`, `:q`                                     | 关闭当前视图。                                                     |
| `:quit!`, `:q!`                                   | 强制关闭当前视图，忽略未保存的修改。                                          |
| `:open`, `:o`, `:edit`, `:e`                      | 从磁盘打开文件到当前视图。                                               |
| `:buffer-close`, `:bc`, `:bclose`                 | 关闭当前缓冲区。                                                    |
| `:buffer-close!`, `:bc!`, `:bclose!`              | 强制关闭当前缓冲区，忽略未保存的修改。                                         |
| `:buffer-close-others`, `:bco`, `:bcloseother`    | 关闭除当前缓冲区外的所有缓冲区。                                            |
| `:buffer-close-others!`, `:bco!`, `:bcloseother!` | 强制关闭除当前缓冲区外的所有缓冲区。                                          |
| `:buffer-close-all`, `:bca`, `:bcloseall`         | 关闭所有缓冲区，但不退出编辑器。                                            |
| `:buffer-close-all!`, `:bca!`, `:bcloseall!`      | 强制关闭所有缓冲区，忽略未保存修改，不退出编辑器。                                   |
| `:buffer-next`, `:bn`, `:bnext`                   | 跳转到下一个缓冲区。                                                  |
| `:buffer-previous`, `:bp`, `:bprev`               | 跳转到上一个缓冲区。                                                  |
| `:write`, `:w`                                    | 将缓冲区修改写入磁盘。可带可选路径参数（`:write some/path.txt`）。                |
| `:write!`, `:w!`                                  | 强制写入缓冲区修改到磁盘，必要时创建子目录。可带可选路径参数（`:write! some/path.txt`）。    |
| `:write-buffer-close`, `:wbc`                     | 写入缓冲区修改并关闭缓冲区。可带可选路径参数。                                     |
| `:write-buffer-close!`, `:wbc!`                   | 强制写入缓冲区修改并关闭缓冲区，必要时创建子目录。可带可选路径参数。                          |
| `:new`, `:n`                                      | 创建一个新的临时缓冲区。                                                |
| `:format`, `:fmt`                                 | 使用外部格式化工具或语言服务器格式化文件。                                       |
| `:indent-style`                                   | 设置缩进样式（'t' 表示制表符，1–16 表示空格数）。                               |
| `:line-ending`                                    | 设置文件行结束符，选项：`crlf`、`lf`。                                    |
| `:earlier`, `:ear`                                | 跳回编辑历史中的早期位置。可指定步数或时间段。                                     |
| `:later`, `:lat`                                  | 跳到编辑历史中的后续位置。可指定步数或时间段。                                     |
| `:write-quit`, `:wq`                              | 写入修改并关闭当前视图。可带可选路径参数。                                       |
| `:write-quit!`, `:wq!`                            | 强制写入修改并关闭当前视图。可带可选路径参数。                                     |
| `:write-all`, `:wa`                               | 写入所有缓冲区的修改。                                                 |
| `:write-all!`, `:wa!`                             | 强制写入所有缓冲区修改，必要时创建子目录。                                       |
| `:write-quit-all`, `:wqa`, `:xa`                  | 写入所有缓冲区修改并关闭所有视图。                                           |
| `:write-quit-all!`, `:wqa!`, `:xa!`               | 强制写入所有缓冲区修改并关闭所有视图（忽略未保存修改）。                                |
| `:quit-all`, `:qa`                                | 关闭所有视图。                                                     |
| `:quit-all!`, `:qa!`                              | 强制关闭所有视图，忽略未保存修改。                                           |
| `:cquit`, `:cq`                                   | 带退出码退出（默认 1），可指定整数退出码（`:cq 2`）。                             |
| `:cquit!`, `:cq!`                                 | 强制带退出码退出（默认 1），忽略未保存修改，可指定整数退出码。                            |
| `:theme`                                          | 切换编辑器主题（不带参数显示当前主题）。                                        |
| `:yank-join`                                      | 复制选区并合并，分隔符可选，默认换行符。                                        |
| `:clipboard-yank`                                 | 将主选区复制到系统剪贴板。                                               |
| `:clipboard-yank-join`                            | 将多个选区合并后复制到系统剪贴板，可选分隔符。                                     |
| `:primary-clipboard-yank`                         | 将主选区复制到主剪贴板。                                                |
| `:primary-clipboard-yank-join`                    | 将多个选区合并后复制到主剪贴板，可选分隔符。                                      |
| `:clipboard-paste-after`                          | 从系统剪贴板在选区后粘贴。                                               |
| `:clipboard-paste-before`                         | 从系统剪贴板在选区前粘贴。                                               |
| `:clipboard-paste-replace`                        | 用系统剪贴板内容替换选区。                                               |
| `:primary-clipboard-paste-after`                  | 从主剪贴板在选区后粘贴。                                                |
| `:primary-clipboard-paste-before`                 | 从主剪贴板在选区前粘贴。                                                |
| `:primary-clipboard-paste-replace`                | 用主剪贴板内容替换选区。                                                |
| `:show-clipboard-provider`                        | 在状态栏显示剪贴板提供程序名称。                                            |
| `:change-current-directory`, `:cd`                | 更改当前工作目录。                                                   |
| `:show-directory`, `:pwd`                         | 显示当前工作目录。                                                   |
| `:encoding`                                       | 设置文件编码（基于 [WHATWG 编码规范](https://encoding.spec.whatwg.org)）。 |
| `:character-info`, `:char`                        | 显示主光标下字符的信息。                                                |
| `:reload`, `:rl`                                  | 放弃修改并重新加载文件。                                                |
| `:reload-all`, `:rla`                             | 放弃所有修改并重新加载所有文档。                                            |
| `:update`, `:u`                                   | 仅在文件被修改时写入磁盘。                                               |
| `:lsp-workspace-command`                          | 打开语言服务器工作区命令选择器。                                            |
| `:lsp-restart`                                    | 重启指定语言服务器，或当前文件使用的所有语言服务器。                                  |
| `:lsp-stop`                                       | 停止指定语言服务器，或当前文件使用的所有语言服务器。                                  |
| `:tree-sitter-scopes`                             | 显示 tree-sitter 作用域，主要用于主题和开发。                               |
| `:tree-sitter-highlight-name`                     | 显示光标下 tree-sitter 高亮作用域名称。                                  |
| `:tree-sitter-layers`                             | 显示光标下 Tree-sitter 注入层的语言名称。                                |
| `:debug-start`, `:dbg`                            | 从指定模板和参数启动调试会话。                                             |
| `:debug-remote`, `:dbg-tcp`                       | 通过 TCP 地址连接调试适配器并启动调试会话。                                    |
| `:debug-eval`                                     | 在当前调试上下文中计算表达式。                                             |
| `:vsplit`, `:vs`                                  | 垂直分屏打开文件。                                                   |
| `:vsplit-new`, `:vnew`                            | 垂直分屏打开临时缓冲区。                                                |
| `:hsplit`, `:hs`, `:sp`                           | 水平分屏打开文件。                                                   |
| `:hsplit-new`, `:hnew`                            | 水平分屏打开临时缓冲区。                                                |
| `:tutor`                                          | 打开 Helix 教程。                                                |
| `:goto`, `:g`                                     | 跳转到指定行号。                                                    |
| `:set-language`, `:lang`                          | 设置当前缓冲区语言（不带参数显示当前语言）。                                      |
| `:set-option`, `:set`                             | 运行时设置配置选项。例如禁用智能大小写搜索：`:set search.smart-case false`。       |
| `:toggle-option`, `:toggle`                       | 切换配置选项。例如切换智能大小写搜索：`:toggle search.smart-case`。             |
| `:get-option`, `:get`                             | 获取当前配置选项值。                                                  |
| `:sort`                                           | 对选区进行排序。                                                    |
| `:reflow`                                         | 对选区进行硬换行，指定行宽。                                              |
| `:tree-sitter-subtree`, `:ts-subtree`             | 显示主选区最小 tree-sitter 子树，主要用于调试查询。                            |
| `:config-reload`                                  | 刷新用户配置。                                                     |
| `:config-open`                                    | 打开用户 `config.toml` 文件。                                      |
| `:config-open-workspace`                          | 打开工作区 `config.toml` 文件。                                     |
| `:log-open`                                       | 打开 Helix 日志文件。                                              |
| `:insert-output`                                  | 执行 shell 命令，并在每个选区前插入输出。                                    |
| `:append-output`                                  | 执行 shell 命令，并在每个选区后追加输出。                                    |
| `:pipe`, `:\|`                                    | 将选区内容传入 shell 命令并替换选区。 |
| `:pipe-to`                                        | 将选区内容传入 shell 命令，忽略输出。 |
| `:run-shell-command`, `:sh`, `:!`                 | 执行 shell 命令。 |
| `:reset-diff-change`, `:diffget`, `:diffg`        | 重置光标位置的差异修改。 |
| `:clear-register`                                 | 清空指定寄存器。如果不提供参数，则清空所有寄存器。 |
| `:redraw`                                         | 清空并重新渲染整个界面。 |
| `:move`, `:mv`                                    | 移动当前缓冲区及对应文件到新路径。 |
| `:yank-diagnostic`                                | 将光标下的诊断信息复制到寄存器或默认剪贴板。 |
| `:read`, `:r`                                     | 将文件加载到缓冲区。 |
| `:echo`                                           | 在状态栏打印指定参数。 |
| `:noop`                                           | 不执行任何操作。 |
