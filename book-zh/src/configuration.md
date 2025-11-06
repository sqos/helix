# 配置

要覆盖全局配置参数，请在配置目录中创建一个 `config.toml` 文件：

* Linux 和 Mac: `~/.config/helix/config.toml`
* Windows: `%AppData%\helix\config.toml`

> 💡 你可以在 Helix 的普通模式下输入 `:config-open` 来轻松打开配置文件。

配置示例：

```toml
theme = "onedark"

[editor]
line-number = "relative"
mouse = false

[editor.cursor-shape]
insert = "bar"
normal = "block"
select = "underline"

[editor.file-picker]
hidden = false
```

你可以通过在命令行使用 `-c` 或 `--config` 参数来指定自定义配置文件，例如 `hx -c path/to/custom-config.toml`。
你可以通过执行 `:config-reload` 命令重新加载配置文件。或者在 Unix 系统上，可以通过向 Helix 进程发送 USR1 信号来重新加载，例如使用命令 `pkill -USR1 hx`。

最后，你可以为项目本地创建一个 `config.toml`，放在仓库的 `.helix` 目录下。
其设置会与配置目录中的 `config.toml` 和内置配置进行合并。
