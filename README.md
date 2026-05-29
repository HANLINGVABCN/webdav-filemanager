# WebDAV File Manager

一个精简、零依赖的 Python WebDAV 文件管理服务器。只需 Python 标准库即可运行，支持跨平台使用。

## ✨ 特性 (Features)

- **零依赖**: 仅使用 Python 3 标准库（无需 `pip install`）。
- **Web UI 界面**: 提供简约美观的网页文件管理器，支持长按/右键菜单。
- **基本文件操作**: 上传、下载、复制、移动、删除、重命名，支持新建空白文件或直接创建并写入文本。
- **两种下载模式**: 智能判断环境，支持浏览器原生下载，以及使用前沿 File System Access API 进行边下载边写入的流式大文件下载（节省内存）。
- **临时分享链接**: 支持为文件生成具有有效期的临时下载链接，可安全地向他人分享文件。
- **网络测速功能**: 支持一键创建指定大小的测速生成的稀疏文件（不占用实际磁盘空间），用于随时测试服务器的上下行网络带宽速度。
- **WebDAV 协议支持**: 可使用系统资源管理器、Finder 或第三方 WebDAV 客户端直接挂载。
- **身份验证**: 支持基于 Web 的登录认证与 WebDAV 的 Basic Auth 基础认证。
- **系统信息**: 顶部实时显示磁盘空间容量及使用状态。
- **一键安装**: 提供 Linux/Systemd 守护进程的一键安装与卸载脚本。

## 🚀 启动与使用 (Usage)

### 命令行运行

运行前确保系统已安装 Python 3 (建议 3.8 及以上版本)。

```bash
python3 server.py [选项]
```

**可用参数**:
- `--port PORT`: 指定监听端口，默认为 `8000`。
- `--root DIR`: 指定根目录路径，默认为当前目录。
- `--auth USER:PASS`: 设置访问认证信息，例如 `admin:123456`。

**示例**:
```bash
# 在 8989 端口启动，管理 /data 目录，用户名为 admin，密码为 123456
python3 server.py --port 8989 --root /data --auth admin:123456
```

### Linux 一键服务部署 (Linux Installer)

系统要求: 拥有 `systemd` 的 Linux 发行版。

运行安装脚本，并按向导提示进行配置：
```bash
sudo ./install.sh
```

此脚本会将程序复制到 `/opt/webdav-filemanager`，创建后台守护进程，支持设置端口、根目录和用户名密码，并自动配置开机启动。

## 📁 文件结构

- `server.py`: 核心服务端脚本，包含了 Web 服务器与 WebDAV 逻辑。
- `index.html`: Web界面的前端代码 (内嵌 CSS 与 JS)。
- `install.sh`: 供 Linux 用户使用的快速安装与配置脚本。

## 🔐 注意事项

- **安全性**: 强烈建议不要通过 HTTP 暴露在公网，若要在公网使用此服务，请配合 Nginx 或 Caddy 等应用配置 HTTPS 反向代理。
- **数据文件**: 运行时程序会在脚本同目录生成 `filemanager_state.json` 与 `filemanager_auth.json` 以存储状态配置，注意备份或防止误删。

## 📄 许可 (License)

MIT License
