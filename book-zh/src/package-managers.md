## 软件包管理器

- [软件包管理器](#软件包管理器)
- [Linux](#linux)
  - [Ubuntu/Debian](#ubuntudebian)
  - [Fedora/RHEL](#fedorarhel)
  - [Arch Linux extra](#arch-linux-extra)
  - [NixOS](#nixos)
  - [Flatpak](#flatpak)
  - [Snap](#snap)
  - [AppImage](#appimage)
- [macOS](#macos)
  - [Homebrew Core](#homebrew-core)
  - [MacPorts](#macports)
- [Windows](#windows)
  - [Winget](#winget)
  - [Scoop](#scoop)
  - [Chocolatey](#chocolatey)
  - [MSYS2](#msys2)

[![打包状态](https://repology.org/badge/vertical-allrepos/helix-editor.svg)](https://repology.org/project/helix-editor/versions)

## Linux

可用的第三方软件仓库如下：

### Ubuntu/Debian

从 [release 页面](https://github.com/helix-editor/helix/releases/latest) 安装 Debian 包。

如果你使用的系统版本低于 Ubuntu 22.04、Mint 21 或 Debian 12，可以本地[从源码构建 `.deb` 文件](./building-from-source.md#building-the-debian-package)。

### Fedora/RHEL

```sh
sudo dnf install helix
```

### Arch Linux extra

发布包可在 `extra` 仓库中获得：

```sh
sudo pacman -S helix
```

> 💡 从 `extra` 仓库安装时，使用 `helix` 而不是 `hx` 启动 Helix。
>
> 例如：
>
> ```sh
> helix --health
> ```
>
> 检查健康状态

此外，AUR 中有 [helix-git](https://aur.archlinux.org/packages/helix-git/) 包，可以构建 master 分支。

### NixOS

Helix 可在 [nixpkgs](https://github.com/nixos/nixpkgs) 中通过 `helix` 属性获取，
不稳定通道通常包含最新版本。

Helix 也可作为项目根目录的 [flake](https://wiki.nixos.org/wiki/Flakes) 使用。使用 `nix develop` 启动可复现的开发 shell。每次向 master 推送时，输出都会使用 [Cachix](https://www.cachix.org/) 缓存。flake 配置为默认使用此缓存（首次使用时需接受新设置）。

如果你的 Nix 版本未启用 flakes，[安装 Cachix CLI](https://docs.cachix.org/installation) 并使用 `cachix use helix` 来配置 Nix 尽可能使用缓存输出。

### Flatpak

Helix 可在 [Flathub](https://flathub.org/en-GB/apps/com.helix_editor.Helix) 获取：

```sh
flatpak install flathub com.helix_editor.Helix
flatpak run com.helix_editor.Helix
```

### Snap

Helix 可在 [Snapcraft](https://snapcraft.io/helix) 安装：

```sh
snap install --classic helix
```

这会将 Helix 安装为 `/snap/bin/helix` 和 `/snap/bin/hx`，确保 `/snap/bin` 在你的 `PATH` 中。

### AppImage

使用 Linux [AppImage](https://appimage.org/) 格式安装 Helix。
从 [最新 releases](https://github.com/helix-editor/helix/releases/latest) 页面下载官方 Helix AppImage。

```sh
chmod +x helix-*.AppImage # 设置可执行权限
./helix-*.AppImage # 运行 Helix
```

可选地[添加 `.desktop` 文件](./building-from-source.md#configure-the-desktop-shortcut)。Helix 必须以 `hx` 名称安装到 `PATH` 中，例如：

```sh
mkdir -p "$HOME/.local/bin"
mv helix-*.AppImage "$HOME/.local/bin/hx"
```

并确保 `~/.local/bin` 在你的 `PATH` 中。

## macOS

### Homebrew Core

```sh
brew install helix
```

### MacPorts

```sh
sudo port install helix
```

## Windows

在 Windows 上可使用 [Winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/)、[Scoop](https://scoop.sh/)、[Chocolatey](https://chocolatey.org/) 或 [MSYS2](https://msys2.org/) 安装。

### Winget

Windows 包管理器 winget 命令行工具在 Windows 11 和新版 Windows 10 中默认可用，作为 App Installer 的一部分。
可从 [Microsoft Store 获取 App Installer](https://www.microsoft.com/p/app-installer/9nblggh4nns1#activetab=pivot:overviewtab)。若已安装，请确保更新至最新版本。

```sh
winget install Helix.Helix
```

### Scoop

```sh
scoop install helix
```

### Chocolatey

```sh
choco install helix
```

### MSYS2

适用于 64 位 Windows 8.1 或更高版本：

```sh
pacman -S mingw-w64-ucrt-x86_64-helix
```
