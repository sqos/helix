# 命令

* [可输入命令](#typable-commands)
* [静态命令](#static-commands)

## 可输入命令

可输入命令在命令模式下使用，并且可以接受参数。命令模式可通过按 `:` 激活。内置的可输入命令有：

{{#include ./generated/typable-cmd.md}}

## 静态命令

静态命令不接受参数，可以绑定到快捷键。静态命令也可以从命令选择器（`<space>?`）中执行。内置的静态命令有：

{{#include ./generated/static-cmd.md}}
