# 安装 Helix

安装 Helix 的常用方式是通过 [你的操作系统的包管理器](./package-managers.md)。

注意：

* 要获取最新的 nightly 版本的 Helix，需要 [从源码构建](./building-from-source.md)。
* 为了充分利用 Helix，安装你所用编程语言的语言服务器。具体操作请参见 [wiki](https://github.com/helix-editor/helix/wiki/Language-Server-Configurations)。

## 预编译二进制文件

从 [GitHub Releases 页面](https://github.com/helix-editor/helix/releases) 下载预编译的二进制文件。
压缩包内容包括 `hx` 可执行文件和 `runtime` 目录。
安装 Helix 的步骤如下：

1. 将 `hx` 可执行文件添加到系统 `$PATH`，以便从命令行使用。
2. 将 `runtime` 目录复制到 `hx` 搜索运行时文件的位置。在 Linux/macOS 上的典型位置是 `~/.config/helix/runtime`。

要查看 `hx` 搜索的运行时目录，请运行 `hx --health`。如有必要，可以通过设置 `HELIX_RUNTIME` 环境变量来覆盖默认运行时位置。
