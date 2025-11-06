## 使用跳转列表

为了便于快速导航，Helix 会维护一个称为 **jumplist（跳转列表）** 的“跳转”列表。
每当你进行一次重要移动（参见下一节）时，Helix 会将移动前的选区存储为一个跳转。

跳转类似于一个检查点，允许你跳到其他位置、进行编辑，然后返回到之前的选区位置。
这样，跳转列表既记录了你之前的位置，也记录了你的选区。

你可以使用 `Ctrl-s` 手动保存一个跳转。
向后跳转使用 `Ctrl-o`，向前跳转使用 `Ctrl-i`。
要查看并选择完整跳转列表，可以使用 `Space-j` 打开跳转列表选择器。

### 什么会生成跳转

以下是会将操作加入跳转列表的动作（非详尽列表）：

* 切换缓冲区

  * 使用缓冲区选择器，跳到上一个/下一个缓冲区
  * 跳到最近访问或修改的文件
  * 创建新文件 (`:new FILE`)
  * 打开文件 (`:open FILE`)

    * 包括 `:log-open`、`:config-open`、`:config-open-workspace`、`:tutor`
  * 通过选择器、全局搜索或文件浏览器导航
  * `goto_file` (`gf`)
* 文件内大幅移动

  * `select_regex` (`s`)
  * `split_regex` (`S`)
  * `search` (`/`)
  * `keep_selections` 和 `remove_selections` (`K` 和 `<A-K>`)
  * `goto_file_start` (`gg`)
  * `goto_file_end`
  * `goto_last_line` (`ge`)
  * `:goto 123` / `:123` / `123G`
  * `goto_definition` (`gd`)
  * `goto_declaration` (`gD`)
  * `goto_type_definition` (`gy`)
  * `goto_reference` (`gr`)
* 其他

  * `Ctrl-s` 手动创建跳转
  * 尝试关闭已修改缓冲区时，会切换到该缓冲区并创建跳转
  * 调试器在跳转堆栈帧时也会生成跳转
