| 名称 | 描述 | 默认按键绑定 |
| ---- | ---- | ---------- |
| `no_op` | 什么也不做 | |
| `move_char_left` | 向左移动 | 普通模式: `h`, `<left>`，插入模式: `<left>` |
| `move_char_right` | 向右移动 | 普通模式: `l`, `<right>`，插入模式: `<right>` |
| `move_line_up` | 向上移动 | 普通模式: `gk` |
| `move_line_down` | 向下移动 | 普通模式: `gj` |
| `move_visual_line_up` | 向上移动 | 普通模式: `k`, `<up>`，插入模式: `<up>` |
| `move_visual_line_down` | 向下移动 | 普通模式: `j`, `<down>`，插入模式: `<down>` |
| `extend_char_left` | 向左扩展 | 选择模式: `h`, `<left>` |
| `extend_char_right` | 向右扩展 | 选择模式: `l`, `<right>` |
| `extend_line_up` | 向上扩展 | 选择模式: `gk` |
| `extend_line_down` | 向下扩展 | 选择模式: `gj` |
| `extend_visual_line_up` | 向上扩展 | 选择模式: `k`, `<up>` |
| `extend_visual_line_down` | 向下扩展 | 选择模式: `j`, `<down>` |
| `copy_selection_on_next_line` | 将选中内容复制到下一行 | 普通模式: `C`, 选择模式: `C` |
| `copy_selection_on_prev_line` | 将选中内容复制到上一行 | 普通模式: `<A-C>`, 选择模式: `<A-C>` |
| `move_next_word_start` | 移动到下一个单词开头 | 普通模式: `w` |
| `move_prev_word_start` | 移动到上一个单词开头 | 普通模式: `b` |
| `move_next_word_end` | 移动到下一个单词结尾 | 普通模式: `e` |
| `move_prev_word_end` | 移动到上一个单词结尾 | |
| `move_next_long_word_start` | 移动到下一个长单词开头 | 普通模式: `W` |
| `move_prev_long_word_start` | 移动到上一个长单词开头 | 普通模式: `B` |
| `move_next_long_word_end` | 移动到下一个长单词结尾 | 普通模式: `E` |
| `move_prev_long_word_end` | 移动到上一个长单词结尾 | |
| `move_next_sub_word_start` | 移动到下一个子单词开头 | |
| `move_prev_sub_word_start` | 移动到上一个子单词开头 | |
| `move_next_sub_word_end` | 移动到下一个子单词结尾 | |
| `move_prev_sub_word_end` | 移动到上一个子单词结尾 | |
| `move_parent_node_end` | 移动到父节点结尾 | 普通模式: `<A-e>` |
| `move_parent_node_start` | 移动到父节点开头 | 普通模式: `<A-b>` |
| `extend_next_word_start` | 扩展到下一个单词开头 | 选择模式: `w` |
| `extend_prev_word_start` | 扩展到上一个单词开头 | 选择模式: `b` |
| `extend_next_word_end` | 扩展到下一个单词结尾 | 选择模式: `e` |
| `extend_prev_word_end` | 扩展到上一个单词结尾 | |
| `extend_next_long_word_start` | 扩展到下一个长单词开头 | 选择模式: `W` |
| `extend_prev_long_word_start` | 扩展到上一个长单词开头 | 选择模式: `B` |
| `extend_next_long_word_end` | 扩展到下一个长单词结尾 | 选择模式: `E` |
| `extend_prev_long_word_end` | 扩展到上一个长单词结尾 | |
| `extend_next_sub_word_start` | 扩展到下一个子单词开头 | |
| `extend_prev_sub_word_start` | 扩展到上一个子单词开头 | |
| `extend_next_sub_word_end` | 扩展到下一个子单词结尾 | |
| `extend_prev_sub_word_end` | 扩展到上一个子单词结尾 | |
| `extend_parent_node_end` | 扩展到父节点结尾 | 选择模式: `<A-e>` |
| `extend_parent_node_start` | 扩展到父节点开头 | 选择模式: `<A-b>` |
| `find_till_char` | 移动到下一个指定字符之前 | 普通模式: `t` |
| `find_next_char` | 移动到下一个指定字符 | 普通模式: `f` |
| `extend_till_char` | 扩展到下一个指定字符之前 | 选择模式: `t` |
| `extend_next_char` | 扩展到下一个指定字符 | 选择模式: `f` |
| `till_prev_char` | 移动到上一个指定字符之前 | 普通模式: `T` |
| `find_prev_char` | 移动到上一个指定字符 | 普通模式: `F` |
| `extend_till_prev_char` | 扩展到上一个指定字符之前 | 选择模式: `T` |
| `extend_prev_char` | 扩展到上一个指定字符 | 选择模式: `F` |
| `repeat_last_motion` | 重复上一次移动 | 普通模式: `<A-.>`, 选择模式: `<A-.>` |
| `replace` | 替换为新字符 | 普通模式: `r`, 选择模式: `r` |
| `switch_case` | 切换大小写 | 普通模式: `~`, 选择模式: `~` |
| `switch_to_uppercase` | 转为大写 | 普通模式: ``<A-`>``, 选择模式: ``<A-`>`` |
| `switch_to_lowercase` | 转为小写 | 普通模式: `` ` ``, 选择模式: `` ` `` |
| `page_up` | 向上翻页 | 普通模式: `<C-b>`, `Z<C-b>`, `z<C-b>`, `<pageup>`, `Z<pageup>`, `z<pageup>`，选择模式: 同上，插入模式: `<pageup>` |
| `page_down` | 向下翻页 | 普通模式: `<C-f>`, `Z<C-f>`, `z<C-f>`, `<pagedown>`, `Z<pagedown>`, `z<pagedown>`，选择模式: 同上，插入模式: `<pagedown>` |
| `half_page_up` | 向上翻半页 | |
| `half_page_down` | 向下翻半页 | |
| `page_cursor_up` | 翻页并移动光标向上 | |
| `page_cursor_down` | 翻页并移动光标向下 | |
| `page_cursor_half_up` | 翻半页并移动光标向上 | 普通模式: `<C-u>`, `Z<C-u>`, `z<C-u>`, `Z<backspace>`, `z<backspace>`，选择模式: 同上 |
| `page_cursor_half_down` | 翻半页并移动光标向下 | 普通模式: `<C-d>`, `Z<C-d>`, `z<C-d>`, `Z<space>`, `z<space>`，选择模式: 同上 |
| `select_all` | 全选文档 | 普通模式: `%`, 选择模式: `%` |
| `select_regex` | 选择匹配正则的内容 | 普通模式: `s`, 选择模式: `s` |
| `split_selection` | 按正则分割选区 | 普通模式: `S`, 选择模式: `S` |
| `split_selection_on_newline` | 按换行分割选区 | 普通模式: `<A-s>`, 选择模式: `<A-s>` |
| `merge_selections` | 合并选区 | 普通模式: `<A-minus>`, 选择模式: `<A-minus>` |
| `merge_consecutive_selections` | 合并连续选区 | 普通模式: `<A-_>`, 选择模式: `<A-_>` |
| `search` | 搜索正则 | 普通模式: `/`, `Z/`, `z/`, 选择模式: 同上 |
| `rsearch` | 反向搜索正则 | 普通模式: `?`, `Z?`, `z?`, 选择模式: 同上 |
| `search_next` | 选中下一个搜索匹配 | 普通模式: `n`, `Zn`, `zn`, 选择模式: `Zn`, `zn` |
| `search_prev` | 选中上一个搜索匹配 | 普通模式: `N`, `ZN`, `zN`, 选择模式: `ZN`, `zN` |
| `extend_search_next` | 将下一个搜索匹配加入选区 | 选择模式: `n` |
| `extend_search_prev` | 将上一个搜索匹配加入选区 | 选择模式: `N` |
| `search_selection` | 使用当前选区作为搜索模式 | 普通模式: `<A-*>`, 选择模式: `<A-*>` |
| `search_selection_detect_word_boundaries` | 使用当前选区作为搜索模式，并在单词边界自动加 `\b` | 普通模式: `*`, 选择模式: `*` |
| `make_search_word_bounded` | 修改当前搜索，使其按单词边界匹配 | |
| `global_search` | 全局搜索工作区 | 普通模式: `<space>/`, 选择模式: `<space>/` |
| `extend_line` | 选择当前行，若已选，则根据锚点扩展 | |
| `extend_line_below` | 选择当前行，若已选，则扩展到下一行 | 普通模式: `x`, 选择模式: `x` |
| `extend_line_above` | 选择当前行，若已选，则扩展到上一行 | |
| `select_line_above` | 选择当前行，若已选，则根据锚点扩展或收缩上一行 | |
| `select_line_below` | 选择当前行，若已选，则根据锚点扩展或收缩下一行 | |
| `extend_to_line_bounds` | 扩展选区到行边界 | 普通模式: `X`, 选择模式: `X` |
| `shrink_to_line_bounds` | 收缩选区到行边界 | 普通模式: `<A-x>`, 选择模式: `<A-x>` |
| `delete_selection` | 删除选区 | 普通模式: `d`, 选择模式: `d` |
| `delete_selection_noyank` | 删除选区且不复制 | 普通模式: `<A-d>`, 选择模式: `<A-d>` |
| `change_selection` | 修改选区 | 普通模式: `c`, 选择模式: `c` |
| `change_selection_noyank` | 修改选区且不复制 | 普通模式: `<A-c>`, 选择模式: `<A-c>` |
| `collapse_selection` | 将选区收缩为单个光标 | 普通模式: `;`, 选择模式: `;` |
| `flip_selections` | 翻转光标和锚点 | 普通模式: `<A-;>`, 选择模式: `<A-;>` |
| `ensure_selections_forward` | 确保所有选区朝向前方 | 普通模式: `<A-:>`, 选择模式: `<A-:>` |
| `insert_mode` | 在选区前插入 | 普通模式: `i`, 选择模式: `i` |
| `append_mode` | 在选区后追加 | 普通模式: `a`, 选择模式: `a` |
| `command_mode` | 进入命令模式 | 普通模式: `:`, 选择模式: `:` |
| `file_picker` | 打开文件选择器 | 普通模式: `<space>f`, 选择模式: `<space>f` |
| `file_picker_in_current_buffer_directory` | 在当前缓冲目录打开文件选择器 | |
| `file_picker_in_current_directory` | 在当前工作目录打开文件选择器 | 普通模式: `<space>F`, 选择模式: `<space>F` |
| `file_explorer` | 在工作区根目录打开文件管理器 | 普通模式: `<space>e`, 选择模式: `<space>e` |
| `file_explorer_in_current_buffer_directory` | 在当前缓冲目录打开文件管理器 | 普通模式: `<space>E`, 选择模式: `<space>E` |
| `file_explorer_in_current_directory` | 在当前工作目录打开文件管理器 | |
| `code_action` | 执行代码操作 | 普通模式: `<space>a`, 选择模式: `<space>a` |
| `buffer_picker` | 打开缓冲区选择器 | 普通模式: `<space>b`, 选择模式: `<space>b` |
| `jumplist_picker` | 打开跳转列表选择器 | 普通模式: `<space>j`, 选择模式: `<space>j` |
| `symbol_picker` | 打开符号选择器 | |
| `syntax_symbol_picker` | 从语法信息打开符号选择器 | |
| `lsp_or_syntax_symbol_picker` | 从 LSP 或语法信息打开符号选择器 | 普通模式: `<space>s`, 选择模式: `<space>s` |
| `changed_file_picker` | 打开已修改文件选择器 | 普通模式: `<space>g`, 选择模式: `<space>g` |
| `select_references_to_symbol_under_cursor` | 选择符号引用 | 普通模式: `<space>h`, 选择模式: `<space>h` |
| `workspace_symbol_picker` | 打开工作区符号选择器 | |
| `syntax_workspace_symbol_picker` | 从语法信息打开工作区符号选择器 | |
| `lsp_or_syntax_workspace_symbol_picker` | 从 LSP 或语法信息打开工作区符号选择器 | 普通模式: `<space>S`, 选择模式: `<space>S` |
| `diagnostics_picker` | 打开诊断选择器 | 普通模式: `<space>d`, 选择模式: `<space>d` |
| `workspace_diagnostics_picker` | 打开工作区诊断选择器 | 普通模式: `<space>D`, 选择模式: `<space>D` |
| `last_picker` | 打开上一个选择器 | 普通模式: `<space>'`, 选择模式: `<space>'` |
| `insert_at_line_start` | 在行首插入 | 普通模式: `I`, 选择模式: `I` |
| `insert_at_line_end` | 在行尾插入 | 普通模式: `A`, 选择模式: `A` |
| `open_below` | 在选区下方新开一行 | 普通模式: `o`, 选择模式: `o` |
| `open_above` | 在选区上方新开一行 | 普通模式: `O`, 选择模式: `O` |
| `normal_mode` | 进入普通模式 | 普通模式: `<esc>`, 选择模式: `v`, 插入模式: `<esc>` |
| `select_mode` | 进入选区扩展模式 | 普通模式: `v` |
| `exit_select_mode` | 退出选区模式 | 选择模式: `<esc>` |
| `goto_definition` | 跳转到定义 | 普通模式: `gd`, 选择模式: `gd` |
| `goto_declaration` | 跳转到声明 | 普通模式: `gD`, 选择模式: `gD` |
| `add_newline_above` | 在上方添加新行 | 普通模式: `[<space>`, 选择模式: `[<space>` |
| `add_newline_below` | 在下方添加新行 | 普通模式: `]<space>`, 选择模式: `]<space>` |
| `goto_type_definition` | 跳转到类型定义 | 普通模式: `gy`, 选择模式: `gy` |
| `goto_implementation` | 跳转到实现 | 普通模式: `gi`, 选择模式: `gi` |
| `goto_file_start` | 跳转到指定行号或文件开头 | 普通模式: `gg` |
| `goto_file_end` | 跳转到文件末尾 | |
| `extend_to_file_start` | 扩展到指定行号或文件开头 | 选择模式: `gg` |
| `extend_to_file_end` | 扩展到文件末尾 | |
| `goto_file` | 跳转到选区中的文件/URL | 普通模式: `gf`, 选择模式: `gf` |
| `goto_file_hsplit` | 横向分割打开选区文件 | 普通模式: `<C-w>f`, `<space>wf`, 选择模式: 同上 |
| `goto_file_vsplit` | 纵向分割打开选区文件 | 普通模式: `<C-w>F`, `<space>wF`, 选择模式: 同上 |
| `goto_reference` | 跳转到引用 | 普通模式: `gr`, 选择模式: `gr` |
| `goto_window_top` | 跳转到窗口顶部 | 普通模式: `gt`, 选择模式: `gt` |
| `goto_window_center` | 跳转到窗口中心 | 普通模式: `gc`, 选择模式: `gc` |
| `goto_window_bottom` | 跳转到窗口底部 | 普通模式: `gb`, 选择模式: `gb` |
| `goto_last_accessed_file` | 跳转到最后访问的文件 | 普通模式: `ga`, 选择模式: `ga` |
| `goto_last_modified_file` | 跳转到最后修改的文件 | 普通模式: `gm`, 选择模式: `gm` |
| `goto_last_modification` | 跳转到最后修改位置 | 普通模式: `g.`, 选择模式: `g.` |
| `goto_line` | 跳转到指定行 | 普通模式: `G`, 选择模式: `G` |
| `goto_last_line` | 跳转到最后一行 | 普通模式: `ge` |
| `extend_to_last_line` | 扩展到最后一行 | 选择模式: `ge` |
| `goto_first_diag` | 跳转到第一个诊断 | 普通模式: `[D`, 选择模式: `[D` |
| `goto_last_diag` | 跳转到最后一个诊断 | 普通模式: `]D`, 选择模式: `]D` |
| `goto_next_diag` | 跳转到下一个诊断 | 普通模式: `]d`, 选择模式: `]d` |
| `goto_prev_diag` | 跳转到上一个诊断 | 普通模式: `[d`, 选择模式: `[d` |
| `goto_next_change` | 跳转到下一个修改 | 普通模式: `]g`, 选择模式: `]g` |
| `goto_prev_change` | 跳转到上一个修改 | 普通模式: `[g`, 选择模式: `[g` |
| `goto_first_change` | 跳转到第一个修改 | 普通模式: `[G`, 选择模式: `[G` |
| `goto_last_change` | 跳转到最后一个修改 | 普通模式: `]G`, 选择模式: `]G` |
| `goto_line_start` | 跳转到行首 | 普通模式: `gh`, `<home>`, 选择模式: `gh`, 插入模式: `<home>` |
| `goto_line_end` | 跳转到行尾 | 普通模式: `gl`, `<end>`, 选择模式: `gl` |
| `goto_column` | 跳转到指定列 | 普通模式: `g\|` |
| `extend_to_column` | 扩展到指定列 | 选择模式: `g\|` |
| `goto_next_buffer` | 跳转到下一个缓冲区 | 普通模式: `gn`, 选择模式: `gn` |
| `goto_previous_buffer` | 跳转到上一个缓冲区 | 普通模式: `gp`, 选择模式: `gp` |
| `goto_line_end_newline` | 跳转到行尾新行 | 插入模式: `<end>` |
| `goto_first_nonwhitespace` | 跳转到行首非空字符 | 普通模式: `gs`, 选择模式: `gs` |
| `trim_selections` | 去除选区空白 | 普通模式: `_`, 选择模式: `_` |
| `extend_to_line_start` | 扩展到行首 | 选择模式: `<home>` |
| `extend_to_first_nonwhitespace` | 扩展到行首非空字符 | |
| `extend_to_line_end` | 扩展到行尾 | 选择模式: `<end>` |
| `extend_to_line_end_newline` | 扩展到行尾 | |
| `signature_help` | 显示签名帮助 | |
| `smart_tab` | 如果光标左侧全为空白则插入 Tab，否则执行其他命令 | 插入模式: `<tab>` |
| `insert_tab` | 插入 Tab 字符 | 插入模式: `<S-tab>` |
| `insert_newline` | 插入换行 | 插入模式: `<C-j>`, `<ret>` |
| `insert_char_interactive` | 交互式插入字符 | |
| `append_char_interactive` | 交互式追加字符 | |
| `delete_char_backward` | 删除前一个字符 | 插入模式: `<C-h>`, `<backspace>`, `<S-backspace>` |
| `delete_char_forward` | 删除下一个字符 | 插入模式: `<C-d>`, `<del>` |
| `delete_word_backward` | 删除前一个单词 | 插入模式: `<C-w>`, `<A-backspace>` |
| `delete_word_forward` | 删除下一个单词 | 插入模式: `<A-d>`, `<A-del>` |
| `kill_to_line_start` | 删除到行首 | 插入模式: `<C-u>` |
| `kill_to_line_end` | 删除到行尾 | 插入模式: `<C-k>` |
| `undo` | 撤销操作 | 普通模式: `u`, 选择模式: `u` |
| `redo` | 重做操作 | 普通模式: `U`, 选择模式: `U` |
| `earlier` | 历史回退 | 普通模式: `<A-u>`, 选择模式: `<A-u>` |
| `later` | 历史前进 | 普通模式: `<A-U>`, 选择模式: `<A-U>` |
| `commit_undo_checkpoint` | 提交更改为新检查点 | 插入模式: `<C-s>` |
| `yank` | 复制选区 | 普通模式: `y`, 选择模式: `y` |
| `yank_to_clipboard` | 复制选区到剪贴板 | 普通模式: `<space>y`, 选择模式: `<space>y` |
| `yank_to_primary_clipboard` | 复制选区到主剪贴板 | |
| `yank_joined` | 合并并复制选区 | |
| `yank_joined_to_clipboard` | 合并并复制选区到剪贴板 | |
| `yank_main_selection_to_clipboard` | 将主选区复制到剪贴板 | 普通模式: `<space>Y`, 选择模式: `<space>Y` |
| `yank_joined_to_primary_clipboard` | 合并并复制到主剪贴板 | |
| `yank_main_selection_to_primary_clipboard` | 将主选区复制到主剪贴板 | |
| `replace_with_yanked` | 用复制内容替换 | 普通模式: `R`, 选择模式: `R` |
| `replace_selections_with_clipboard` | 用剪贴板内容替换选区 | 普通模式: `<space>R`, 选择模式: `<space>R` |
| `replace_selections_with_primary_clipboard` | 用主剪贴板内容替换选区 | |
| `paste_after` | 在选区后粘贴 | 普通模式: `p`, 选择模式: `p` |
| `paste_before` | 在选区前粘贴 | 普通模式: `P`, 选择模式: `P` |
| `paste_clipboard_after` | 在选区后粘贴剪贴板内容 | 普通模式: `<space>p`, 选择模式: `<space>p` |
| `paste_clipboard_before` | 在选区前粘贴剪贴板内容 | 普通模式: `<space>P`, 选择模式: `<space>P` |
| `paste_primary_clipboard_after` | 在选区后粘贴主剪贴板内容 | |
| `paste_primary_clipboard_before` | 在选区前粘贴主剪贴板内容 | |
| `indent` | 缩进选区 | 普通模式: `<gt>`, 选择模式: `<gt>` |
| `unindent` | 取消缩进选区 | 普通模式: `<lt>`, 选择模式: `<lt>` |
| `format_selections` | 格式化选区 | 普通模式: `=`, 选择模式: `=` |
| `join_selections` | 合并选区内行 | 普通模式: `J`, 选择模式: `J` |
| `join_selections_space` | 合并选区内行并保留空格 | 普通模式: `<A-J>`, 选择模式: `<A-J>` |
| `keep_selections` | 保留匹配正则的选区 | 普通模式: `K`, 选择模式: `K` |
| `remove_selections` | 移除匹配正则的选区 | 普通模式: `<A-K>`, 选择模式: `<A-K>` |
| `align_selections` | 对齐选区列 | 普通模式: `&`, 选择模式: `&` |
| `keep_primary_selection` | 保留主选区 | 普通模式: `,`, 选择模式: `,` |
| `remove_primary_selection` | 移除主选区 | 普通模式: `<A-,>`, 选择模式: `<A-,>` |
| `completion` | 调出补全弹窗 | 插入模式: `<C-x>` |
| `hover` | 显示光标下项的文档 | 普通模式: `<space>k`, 选择模式: `<space>k` |
| `toggle_comments` | 注释/取消注释选区 | 普通模式: `<C-c>`, `<space>c`, 选择模式: `<C-c>`, `<space>c` |
| `toggle_line_comments` | 注释/取消注释行 | 普通模式: `<space><A-c>`, 选择模式: `<space><A-c>` |
| `toggle_block_comments` | 注释/取消注释块 | 普通模式: `<space>C`, 选择模式: `<space>C` |
| `rotate_selections_forward` | 选区前移 | 普通模式: `)`, 选择模式: `)` |
| `rotate_selections_backward` | 选区后移 | 普通模式: `(`, 选择模式: `(` |
| `rotate_selection_contents_forward` | 选区内容前移 | 普通模式: `<A-)>`, 选择模式: `<A-)>` |
| `rotate_selection_contents_backward` | 选区内容后移 | 普通模式: `<A-(>`, 选择模式: `<A-(>` |
| `reverse_selection_contents` | 反转选区内容 | |
| `expand_selection` | 扩展选区到父语法节点 | 普通模式: `<A-o>`, `<A-up>`, 选择模式: `<A-o>`, `<A-up>` |
| `shrink_selection` | 缩小选区到之前扩展的语法节点 | 普通模式: `<A-i>`, `<A-down>`, 选择模式: `<A-i>`, `<A-down>` |
| `select_next_sibling` | 选择语法树中的下一个同级节点 | 普通模式: `<A-n>`, `<A-right>`, 选择模式: `<A-n>`, `<A-right>` |
| `select_prev_sibling` | 选择语法树中的上一个同级节点 | 普通模式: `<A-p>`, `<A-left>`, 选择模式: `<A-p>`, `<A-left>` |
| `select_all_siblings` | 选择当前节点的所有同级节点 | 普通模式: `<A-a>`, 选择模式: `<A-a>` |
| `select_all_children` | 选择当前节点的所有子节点 | 普通模式: `<A-I>`, `<S-A-down>`, 选择模式: `<A-I>`, `<S-A-down>` |
| `jump_forward` | 跳转到跳转列表的前一个位置 | 普通模式: `<C-i>`, `<tab>`, 选择模式: `<C-i>`, `<tab>` |
| `jump_backward` | 跳转到跳转列表的后一个位置 | 普通模式: `<C-o>`, 选择模式: `<C-o>` |
| `save_selection` | 将当前选区保存到跳转列表 | 普通模式: `<C-s>`, 选择模式: `<C-s>` |
| `jump_view_right` | 跳转到右侧窗口 | 普通模式: `<C-w>l`, `<space>wl`, `<C-w><C-l>`, `<C-w><right>`, `<space>w<C-l>`, `<space>w<right>`, 选择模式: 同上 |
| `jump_view_left` | 跳转到左侧窗口 | 普通模式: `<C-w>h`, `<space>wh`, `<C-w><C-h>`, `<C-w><left>`, `<space>w<C-h>`, `<space>w<left>`, 选择模式: 同上 |
| `jump_view_up` | 跳转到上方窗口 | 普通模式: `<C-w>k`, `<C-w><up>`, `<space>wk`, `<C-w><C-k>`, `<space>w<up>`, `<space>w<C-k>`, 选择模式: 同上 |
| `jump_view_down` | 跳转到下方窗口 | 普通模式: `<C-w>j`, `<space>wj`, `<C-w><C-j>`, `<C-w><down>`, `<space>w<C-j>`, `<space>w<down>`, 选择模式: 同上 |
| `swap_view_right` | 与右侧窗口交换 | 普通模式: `<C-w>L`, `<space>wL`, 选择模式: `<C-w>L`, `<space>wL` |
| `swap_view_left` | 与左侧窗口交换 | 普通模式: `<C-w>H`, `<space>wH`, 选择模式: `<C-w>H`, `<space>wH` |
| `swap_view_up` | 与上方窗口交换 | 普通模式: `<C-w>K`, `<space>wK`, 选择模式: `<C-w>K`, `<space>wK` |
| `swap_view_down` | 与下方窗口交换 | 普通模式: `<C-w>J`, `<space>wJ`, 选择模式: `<C-w>J`, `<space>wJ` |
| `transpose_view` | 转置分屏 | 普通模式: `<C-w>t`, `<space>wt`, `<C-w><C-t>`, `<space>w<C-t>`, 选择模式: 同上 |
| `rotate_view` | 跳转到下一个窗口 | 普通模式: `<C-w>w`, `<space>ww`, `<C-w><C-w>`, `<space>w<C-w>`, 选择模式: 同上 |
| `rotate_view_reverse` | 跳转到上一个窗口 | |
| `hsplit` | 水平底部分屏 | 普通模式: `<C-w>s`, `<space>ws`, `<C-w><C-s>`, `<space>w<C-s>`, 选择模式: 同上 |
| `hsplit_new` | 水平底部分屏（临时缓冲区） | 普通模式: `<C-w>ns`, `<space>wns`, `<C-w>n<C-s>`, `<space>wn<C-s>`, 选择模式: 同上 |
| `vsplit` | 垂直右部分屏 | 普通模式: `<C-w>v`, `<space>wv`, `<C-w><C-v>`, `<space>w<C-v>`, 选择模式: 同上 |
| `vsplit_new` | 垂直右部分屏（临时缓冲区） | 普通模式: `<C-w>nv`, `<space>wnv`, `<C-w>n<C-v>`, `<space>wn<C-v>`, 选择模式: 同上 |
| `wclose` | 关闭窗口 | 普通模式: `<C-w>q`, `<space>wq`, `<C-w><C-q>`, `<space>w<C-q>`, 选择模式: 同上 |
| `wonly` | 除当前窗口外关闭所有窗口 | 普通模式: `<C-w>o`, `<space>wo`, `<C-w><C-o>`, `<space>w<C-o>`, 选择模式: 同上 |
| `select_register` | 选择寄存器 | 普通模式: `"`, 选择模式: `"` |
| `insert_register` | 插入寄存器内容 | 插入模式: `<C-r>` |
| `copy_between_registers` | 在两个寄存器间复制 | |
| `align_view_middle` | 居中对齐视图 | 普通模式: `Zm`, `zm`, 选择模式: 同上 |
| `align_view_top` | 顶部对齐视图 | 普通模式: `Zt`, `zt`, 选择模式: 同上 |
| `align_view_center` | 中心对齐视图 | 普通模式: `Zc`, `Zz`, `zc`, `zz`, 选择模式: 同上 |
| `align_view_bottom` | 底部对齐视图 | 普通模式: `Zb`, `zb`, 选择模式: 同上 |
| `scroll_up` | 向上滚动视图 | 普通模式: `Zk`, `zk`, `Z<up>`, `z<up>`, 选择模式: 同上 |
| `scroll_down` | 向下滚动视图 | 普通模式: `Zj`, `zj`, `Z<down>`, `z<down>`, 选择模式: 同上 |
| `match_brackets` | 跳转到匹配括号 | 普通模式: `mm`, 选择模式: `mm` |
| `surround_add` | 添加包围符 | 普通模式: `ms`, 选择模式: `ms` |
| `surround_replace` | 替换包围符 | 普通模式: `mr`, 选择模式: `mr` |
| `surround_delete` | 删除包围符 | 普通模式: `md`, 选择模式: `md` |
| `select_textobject_around` | 选择对象及其外围 | 普通模式: `ma`, 选择模式: `ma` |
| `select_textobject_inner` | 选择对象内部 | 普通模式: `mi`, 选择模式: `mi` |
| `goto_next_function` | 跳到下一个函数 | 普通模式: `]f`, 选择模式: `]f` |
| `goto_prev_function` | 跳到上一个函数 | 普通模式: `[f`, 选择模式: `[f` |
| `goto_next_class` | 跳到下一个类型定义 | 普通模式: `]t`, 选择模式: `]t` |
| `goto_prev_class` | 跳到上一个类型定义 | 普通模式: `[t`, 选择模式: `[t` |
| `goto_next_parameter` | 跳到下一个参数 | 普通模式: `]a`, 选择模式: `]a` |
| `goto_prev_parameter` | 跳到上一个参数 | 普通模式: `[a`, 选择模式: `[a` |
| `goto_next_comment` | 跳到下一个注释 | 普通模式: `]c`, 选择模式: `]c` |
| `goto_prev_comment` | 跳到上一个注释 | 普通模式: `[c`, 选择模式: `[c` |
| `goto_next_test` | 跳到下一个测试 | 普通模式: `]T`, 选择模式: `]T` |
| `goto_prev_test` | 跳到上一个测试 | 普通模式: `[T`, 选择模式: `[T` |
| `goto_next_xml_element` | 跳到下一个 (X)HTML 元素 | 普通模式: `]x`, 选择模式: `]x` |
| `goto_prev_xml_element` | 跳到上一个 (X)HTML 元素 | 普通模式: `[x`, 选择模式: `[x` |
| `goto_next_entry` | 跳到下一个配对 | 普通模式: `]e`, 选择模式: `]e` |
| `goto_prev_entry` | 跳到上一个配对 | 普通模式: `[e`, 选择模式: `[e` |
| `goto_next_paragraph` | 跳到下一个段落 | 普通模式: `]p`, 选择模式: `]p` |
| `goto_prev_paragraph` | 跳到上一个段落 | 普通模式: `[p`, 选择模式: `[p` |
| `dap_launch` | 启动调试目标 | 普通模式: `<space>Gl`, 选择模式: `<space>Gl` |
| `dap_restart` | 重启调试会话 | 普通模式: `<space>Gr`, 选择模式: `<space>Gr` |
| `dap_toggle_breakpoint` | 切换断点 | 普通模式: `<space>Gb`, 选择模式: `<space>Gb` |
| `dap_continue` | 继续程序执行 | 普通模式: `<space>Gc`, 选择模式: `<space>Gc` |
| `dap_pause` | 暂停程序执行 | 普通模式: `<space>Gh`, 选择模式: `<space>Gh` |
| `dap_step_in` | 单步进入 | 普通模式: `<space>Gi`, 选择模式: `<space>Gi` |
| `dap_step_out` | 单步跳出 | 普通模式: `<space>Go`, 选择模式: `<space>Go` |
| `dap_next` | 单步执行到下一个 | 普通模式: `<space>Gn`, 选择模式: `<space>Gn` |
| `dap_variables` | 列出变量 | 普通模式: `<space>Gv`, 选择模式: `<space>Gv` |
| `dap_terminate` | 结束调试会话 | 普通模式: `<space>Gt`, 选择模式: `<space>Gt` |
| `dap_edit_condition` | 编辑当前行断点条件 | 普通模式: `<space>G<C-c>`, 选择模式: `<space>G<C-c>` |
| `dap_edit_log` | 编辑当前行断点日志 | 普通模式: `<space>G<C-l>`, 选择模式: `<space>G<C-l>` |
| `dap_switch_thread` | 切换当前线程 | 普通模式: `<space>Gst`, 选择模式: `<space>Gst` |
| `dap_switch_stack_frame` | 切换栈帧 | 普通模式: `<space>Gsf`, 选择模式: `<space>Gsf` |
| `dap_enable_exceptions` | 启用异常断点 | 普通模式: `<space>Ge`, 选择模式: `<space>Ge` |
| `dap_disable_exceptions` | 禁用异常断点 | 普通模式: `<space>GE`, 选择模式: `<space>GE` |
| `shell_pipe` | 将选区通过 Shell 命令管道 | 普通模式: `\|`, 选择模式: `\|` |
| `shell_pipe_to` | 将选区管道到 Shell 命令并忽略输出 | 普通模式: `<A-\|>`, 选择模式: `<A-\|>` |
| `shell_insert_output` | 在选区前插入 Shell 命令输出 | 普通模式: `!`, 选择模式: `!` |
| `shell_append_output` | 在选区后追加 Shell 命令输出 | 普通模式: `<A-!>`, 选择模式: `<A-!>` |
| `shell_keep_pipe` | 使用 Shell 谓词过滤选区 | 普通模式: `$`, 选择模式: `$` |
| `suspend`| 挂起并返回 Shell | 普通模式: `` <C-z> ``, 选择模式: `` <C-z> `` |
| `rename_symbol`| 重命名符号 | 普通模式: `` <space>r ``, 选择模式: `` <space>r `` |
| `increment`| 增加光标下项 | 普通模式: `` <C-a> ``, 选择模式: `` <C-a> `` |
| `decrement`| 减少光标下项 | 普通模式: `` <C-x> ``, 选择模式: `` <C-x> `` |
| `record_macro`| 录制宏 | 普通模式: `` Q ``, 选择模式: `` Q `` |
| `replay_macro`| 回放宏 | 普通模式: `` q ``, 选择模式: `` q `` |
| `command_palette`| 打开命令面板 | 普通模式: `` <space>? ``, 选择模式: `` <space>? `` |
| `goto_word`| 跳转到两字符标签 | 普通模式: `` gw `` |
| `extend_to_word`| 扩展到两字符标签 | 选择模式: `` gw `` |
| `goto_next_tabstop`| 跳到下一个代码片段占位符 | |
| `goto_prev_tabstop`| 跳到上一个代码片段占位符 | |
| `rotate_selections_first`| 将第一个选区设为主选区 | |
| `rotate_selections_last` | 将最后一个选区设为主选区 | |

