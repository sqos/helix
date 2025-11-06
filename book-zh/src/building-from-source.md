## 从源码构建

* [配置 Helix 的运行时文件](#configuring-helixs-runtime-files)

  * [Linux 和 macOS](#linux-and-macos)
  * [Windows](#windows)
  * [多个运行时目录](#multiple-runtime-directories)
  * [打包者注意事项](#note-to-packagers)
* [验证安装](#validating-the-installation)
* [配置桌面快捷方式](#configure-the-desktop-shortcut)
* [构建 Debian 软件包](#building-the-debian-package)

要求：

将 Helix 的 GitHub 仓库克隆到你选择的目录中。本文档中的示例假设安装在 Linux 和 macOS 的 `~/src/`，或 Windows 的 `%userprofile%\src\`。

* [Rust 工具链](https://www.rust-lang.org/tools/install)
* [Git 版本控制系统](https://git-scm.com/)
* 支持 C++14 的编译器，用于构建 tree-sitter 语法，例如 GCC 或 Clang

如果使用 `musl-libc` 标准库而非 `glibc`，则必须在构建期间设置以下环境变量，以确保 tree-sitter 语法可以正确加载：

```sh
RUSTFLAGS="-C target-feature=-crt-static"
```

1. 克隆仓库：

   ```sh
   git clone https://github.com/helix-editor/helix
   cd helix
   ```

2. 从源码编译：

   ```sh
   # 可复现版本
   cargo install --path helix-term --locked
   ```

   ```sh
   # 优化版本
   cargo install \
      --profile opt \
      --config 'build.rustflags=["-C", "target-cpu=native"]' \
      --path helix-term \
      --locked
   ```

   任何一条命令都会创建 `hx` 可执行文件，并在本地 `runtime` 文件夹中构建 tree-sitter 语法。

> 💡 如果不想获取或构建语法，请设置环境变量 `HELIX_DISABLE_AUTO_GRAMMAR_BUILD`

> 💡 如果语法未打包，可通过 tree-sitter 获取和编译：
> 使用 `hx --grammar fetch` 获取语法，并用 `hx --grammar build` 编译。
> 这会将其安装到用户 Helix 配置目录下的 `runtime` 目录中（更多
> [详情见下](#multiple-runtime-directories)）。

### 配置 Helix 的运行时文件

#### Linux 和 macOS

**runtime** 目录位于 Helix 源码下方，可以通过导出 `HELIX_RUNTIME` 环境变量指向该目录，并添加到你的 `~/.bashrc` 或等效文件中：

```sh
export HELIX_RUNTIME=~/src/helix/runtime
```

或者，创建符号链接：

```sh
ln -Tsf $PWD/runtime ~/.config/helix/runtime
```

#### Windows

可以通过 Windows 设置（搜索 “编辑你账户的环境变量”）设置 `HELIX_RUNTIME` 环境变量指向运行时文件，
也可以在 Cmd 中使用 `setx` 命令：

```sh
setx HELIX_RUNTIME "%userprofile%\src\helix\runtime"
```

> 💡 `%userprofile%` 会解析为你的用户目录，例如 `C:\Users\Your-Name\\`。

或者，在 `%appdata%\helix\` 中创建一个符号链接，指向源码目录：

| 方法         | 命令                                                                                 |
| ---------- | ---------------------------------------------------------------------------------- |
| PowerShell | `New-Item -ItemType Junction -Target "runtime" -Path "$Env:AppData\helix\runtime"` |
| Cmd        | `cd %appdata%\helix` <br/> `mklink /D runtime "%userprofile%\src\helix\runtime"`   |

> 💡 在 Windows 上，创建符号链接可能需要以管理员身份运行 PowerShell 或 Cmd。

#### 多个运行时目录

当 Helix 发现多个运行时目录时，它会按以下顺序搜索文件：

1. 与 `$CARGO_MANIFEST_DIR` 目录为同级的 `runtime/` 目录（仅用于开发和测试 Helix）。
2. OS 依赖的 Helix 用户配置目录下的 `runtime/` 子目录。
3. `$HELIX_RUNTIME`
4. 发行版特定的备用目录（在编译时设置，而非运行时—通过 `HELIX_DEFAULT_RUNTIME` 环境变量）。
5. Helix 可执行文件路径下的 `runtime/` 子目录。

此顺序还设置了优先级：如果多个运行时目录中存在同名文件，将使用顺序靠前的目录中的文件。

#### 打包者注意事项

如果你为最终用户打包 Helix，为了提供良好的开箱体验，应在构建时（调用 `cargo build` 前）设置 `HELIX_DEFAULT_RUNTIME` 环境变量，指向安装后存放最终运行时文件的目录。例如，你希望将运行时打包到 `/usr/lib/helix/runtime`。构建脚本的大致步骤如下：

1. `export HELIX_DEFAULT_RUNTIME=/usr/lib/helix/runtime`
2. `cargo build --profile opt --locked`
3. `cp -r runtime $BUILD_DIR/usr/lib/helix/`
4. `cp target/opt/hx $BUILD_DIR/usr/bin/hx`

这样生成的 `hx` 二进制文件在用户没有自定义运行时（`~/.config/helix` 或 `HELIX_RUNTIME`）的情况下，会始终查找 `/usr/lib/helix/runtime`。

### 验证安装

为了确保一切按预期设置，应运行 Helix 健康检查：

```sh
hx --health
```

有关健康检查结果的更多信息，请参考
[Health check](https://github.com/helix-editor/helix/wiki/Healthcheck)。

### 配置桌面快捷方式

如果你的桌面环境支持
[XDG 桌面菜单](https://specifications.freedesktop.org/menu-spec/menu-spec-latest.html)
可以通过将提供的 `.desktop` 文件和图标文件复制到正确的文件夹来让 Helix 出现在应用菜单中：

```sh
cp contrib/Helix.desktop ~/.local/share/applications
cp contrib/helix.png ~/.icons # 或 ~/.local/share/icons
```

建议将 `.desktop` 文件中的链接转换为绝对路径，以避免潜在问题：

```sh
sed -i -e "s|Exec=hx %F|Exec=$(readlink -f ~/.cargo/bin/hx) %F|g" \
  -e "s|Icon=helix|Icon=$(readlink -f ~/.icons/helix.png)|g" ~/.local/share/applications/Helix.desktop
```

如果要使用系统默认终端以外的终端，可以修改 `.desktop` 文件。例如，使用 `kitty`：

```sh
sed -i "s|Exec=hx %F|Exec=kitty hx %F|g" ~/.local/share/applications/Helix.desktop
sed -i "s|Terminal=true|Terminal=false|g" ~/.local/share/applications/Helix.desktop
```

### 构建 Debian 软件包

如果发布页面提供的 `.deb` 文件使用的 `libc` 版本高于你的 Debian、Ubuntu 或 Mint 系统所用版本，你可以从源码构建软件包以匹配系统依赖。

安装用于构建 `.deb` 文件的工具 `cargo-deb`：

```sh
cargo install cargo-deb
```

按照前文所述克隆并进入 Helix 仓库后，使用以下命令可在一步中构建发布二进制文件并打包成 `.deb` 文件：

```sh
cargo deb -- --locked
```

> 💡 这会锁定使用 `--release` 配置文件。但你也可以按自己喜欢的方式构建 Helix。
> 只要保留 `target/release/hx` 文件，使用 `cargo deb --no-build` 也能打包。

> 💡 不必担心以下警告：
>
> ```
> warning: Failed to find dependency specification
> ```
>
> Cargo deb 只是报告哪些打包文件未生成依赖关系。到目前为止，依赖关系推导效果良好，即使某些语法文件被跳过。

生成的 `.deb` 文件位于 `target/debian/`。它应包含所需的一切，包括：

* bash、fish、zsh 的补全
* `.desktop` 文件
* 图标（虽然桌面环境可能使用自己的图标，但包名为 `helix`）
* 启动器二进制文件及运行时
