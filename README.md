**声明：主要是对于进程和cpu磁盘的检查，其他功能慎用**
# GeekDISK
## 一、README_LINUX.md
```bash
cd ~/桌面/to-for-playgeek/GeekDash/Projects/GeekDash-Project-v8.0 || exit 1

cat > README_LINUX.md <<'EOF'
# GeekDash Linux

**版本：v1.0.0**

GeekDash 是一款面向 Linux 桌面环境的系统管理与监控工具。

本项目提供 Linux 原生发行包，支持 DEB、RPM 和通用 ZIP 部署方式，提供桌面启动入口，并支持通过独立的 Root Helper 执行需要管理员权限的网络审计操作。

---

## 1. 产品信息

| 项目 | 信息 |
|---|---|
| 产品名称 | GeekDash |
| 文档版本 | v1.0.0 |
| 当前 Linux 构建版本 | 8.0.0 |
| 支持架构 | x86_64 / AMD64 |
| 主要运行环境 | Linux 桌面系统 |
| 图形界面 | PySide6 / Qt |
| 系统监控 | psutil |
| 网络审计 | 独立 Root Helper |
| 权限管理 | Polkit |
| 发布格式 | DEB / RPM / ZIP |

注意：README 文档版本 v1.0.0 与当前安装包内部版本 8.0.0 是不同的版本标识。安装包的实际版本以软件包元数据为准。

---

## 2. 功能概览

GeekDash Linux 版本提供以下功能模块：

- Linux 桌面图形界面。
- 系统运行状态监控。
- CPU、内存等系统资源信息读取。
- 进程与系统运行信息管理。
- 基于 psutil 的系统信息采集。
- 网络审计功能。
- 独立 Root Helper 权限辅助程序。
- Polkit 管理员授权机制。
- GUI 与后台任务生命周期管理。

具体功能以实际发行版本中集成的模块为准。

---

## 3. 系统要求

### 3.1 硬件与系统架构

- 64 位 x86 处理器。
- x86_64 / AMD64 Linux 系统。
- 建议使用具有完整桌面环境的 Linux 发行版。
- 建议至少 4 GB 内存。

### 3.2 软件环境

根据发行包类型，需要满足相应系统依赖。

主要依赖包括：

- GLIBC
- libstdc++
- Qt 相关系统库
- Polkit
- Python 3 运行环境
- psutil

DEB 包会声明对应的 Debian 软件包依赖。

RPM 包会声明对应的 RPM 系统依赖。

ZIP 部署需要根据目标发行版安装必要的系统组件。

### 3.3 兼容性说明

当前 Linux 安装包是在以下环境中构建的：

| 项目 | 构建环境 |
|---|---|
| 操作系统 | Ubuntu |
| 架构 | x86_64 |
| GLIBC | 2.43 |
| Python | 3.14.4 |
| PySide6 | 6.12.0 |
| PyInstaller | 6.22.3 |
| psutil | 7.2.2 |

特别注意：

当前 RPM 包存在 GLIBC_2.43 版本要求，以及 GLIBCXX_3.4.29 等 C++ ABI 版本要求。

因此：

- 不保证兼容 GLIBC 低于 2.43 的系统。
- 不保证兼容所有 Fedora、RHEL、Rocky Linux 和 AlmaLinux 版本。
- 不应仅根据 RPM 包可以成功构建，就判断其能够在所有 RPM 发行版上运行。
- 正式部署前应在目标发行版上完成依赖检查和实际运行测试。

---

## 4. Linux 发行包

发行目录中提供以下文件：

```text
release/
├── geekdash_8.0.0_amd64.deb
├── geekdash-8.0.0-1.x86_64.rpm
├── GeekDash-8.0.0-Linux-x86_64.zip
├── SHA256SUMS.txt
└── build-report.json
```

### 4.1 DEB 安装包

适用于使用 DEB 软件包管理系统的 Linux 发行版。

例如：

- Ubuntu
- Debian
- Linux Mint

安装命令：

```bash
sudo apt install ./geekdash_8.0.0_amd64.deb
```

如果需要先检查软件包信息：

```bash
dpkg-deb -I geekdash_8.0.0_amd64.deb
```

查看安装文件：

```bash
dpkg-deb --contents geekdash_8.0.0_amd64.deb
```

启动程序：

```bash
geekdash
```

也可以从桌面应用程序菜单启动 GeekDash。

### 4.2 RPM 安装包

适用于使用 RPM 软件包管理系统的 Linux 发行版。

例如：

- Fedora
- RHEL
- Rocky Linux
- AlmaLinux

安装命令：

```bash
sudo dnf install ./geekdash-8.0.0-1.x86_64.rpm
```

部分发行版也可以使用：

```bash
sudo rpm -ivh geekdash-8.0.0-1.x86_64.rpm
```

启动程序：

```bash
geekdash
```

注意：

RPM 包的 GLIBC 和 C++ ABI 版本要求必须由目标系统满足。建议优先使用与构建环境兼容的较新发行版，并在目标机器上实际验证。

### 4.3 ZIP 通用部署包

文件：

```text
GeekDash-8.0.0-Linux-x86_64.zip
```

解压：

```bash
unzip GeekDash-8.0.0-Linux-x86_64.zip
```

进入解压目录：

```bash
cd GeekDash-8.0.0-Linux-x86_64
```

查看文件：

```bash
ls -lah
```

根据发行包提供的说明执行安装或启动。

如果需要安装系统级 Helper 和 Polkit 组件，请先检查安装脚本：

```bash
less install-system-components.sh
```

确认脚本内容后，再根据脚本说明和目标发行版要求执行。

不要在未检查脚本内容的情况下直接以 Root 身份执行未知脚本。

---

## 5. 系统组件与权限管理

GeekDash 的高级网络审计功能使用独立的 Root Helper。

相关组件：

```text
/usr/libexec/geekdash/geekdash-net-audit-helper
/usr/share/polkit-1/actions/com.geekdash.net-audit.policy
```

组件作用：

| 组件 | 作用 |
|---|---|
| GeekDash GUI | 提供桌面交互界面 |
| Root Helper | 执行需要管理员权限的网络审计操作 |
| Polkit Policy | 定义管理员授权规则 |
| QProcess | GUI 与 Helper 之间的进程通信 |

### 5.1 权限设计

GeekDash GUI 正常情况下以当前登录用户身份运行。

需要管理员权限的网络审计操作由独立 Helper 负责。

设计原则：

- 不要求整个 GUI 以 Root 身份运行。
- 通过 Polkit 请求管理员授权。
- Helper 使用独立程序运行。
- GUI 与 Helper 通过进程通信。
- 避免将普通用户输入直接作为 Root 命令执行。

### 5.2 Helper 文件权限

安装后可以检查：

```bash
ls -l /usr/libexec/geekdash/geekdash-net-audit-helper
```

预期权限：

```text
-rwxr-xr-x root root
```

检查 Polkit Policy：

```bash
ls -l /usr/share/polkit-1/actions/com.geekdash.net-audit.policy
```

预期文件所有者为 Root，普通用户具有读取权限。

如果组件缺失或权限不正确，高级网络审计功能可能无法正常工作。

---

## 6. 启动 GeekDash

安装完成后，可以通过以下方式启动。

### 方式一：终端启动

```bash
geekdash
```

### 方式二：桌面菜单启动

打开桌面环境的应用程序菜单，搜索：

```text
GeekDash
```

选择 GeekDash 图标启动。

### 方式三：检查运行进程

```bash
pgrep -af geekdash
```

如果程序正常启动，应能够看到相应进程。

---

## 7. 卸载 GeekDash

### 7.1 Ubuntu / Debian

执行：

```bash
sudo apt remove geekdash
```

如果需要删除软件包配置文件：

```bash
sudo apt purge geekdash
```

### 7.2 Fedora / RHEL 系

执行：

```bash
sudo dnf remove geekdash
```

### 7.3 ZIP 部署

ZIP 部署的卸载方式取决于实际安装脚本和部署方式。

卸载前应检查：

- 安装目录。
- 桌面启动文件。
- Root Helper。
- Polkit Policy。
- 用户配置和数据目录。

不要直接删除整个系统目录，也不要在不确认归属的情况下删除共享系统组件。

---

## 8. 完整性验证

官方发行包提供 SHA256 校验文件：

```text
SHA256SUMS.txt
```

在发行包目录执行：

```bash
sha256sum -c SHA256SUMS.txt
```

正常情况下，应显示：

```text
GeekDash-8.0.0-Linux-x86_64.zip: OK
geekdash-8.0.0-1.x86_64.rpm: OK
geekdash_8.0.0_amd64.deb: OK
```

如果出现 FAILED，说明文件与校验记录不一致。

请重新获取完整发行包，不要安装校验失败的文件。

---

## 9. 常见问题

### 9.1 启动时提示缺少系统库

检查系统版本：

```bash
cat /etc/os-release
```

检查 GLIBC：

```bash
ldd --version
```

检查系统依赖：

Ubuntu / Debian：

```bash
sudo apt update
sudo apt --fix-broken install
```

Fedora：

```bash
sudo dnf check
```

请确保目标系统满足发行包的依赖要求。

### 9.2 网络审计功能无法启动

检查 Helper：

```bash
ls -l /usr/libexec/geekdash/geekdash-net-audit-helper
```

检查 Polkit：

```bash
ls -l /usr/share/polkit-1/actions/com.geekdash.net-audit.policy
```

检查 Polkit 服务：

```bash
systemctl status polkit
```

不同发行版的服务名称可能有所不同。

### 9.3 Polkit 授权失败

确认当前用户处于正常的桌面登录会话。

检查系统是否安装 Polkit：

Ubuntu / Debian：

```bash
dpkg -l | grep polkit
```

Fedora：

```bash
rpm -qa | grep polkit
```

如果仍然失败，请检查系统日志：

```bash
journalctl -b | grep -i polkit
```

### 9.4 RPM 安装时提示依赖不满足

检查 RPM 依赖：

```bash
rpm -qp --requires geekdash-8.0.0-1.x86_64.rpm
```

重点检查 GLIBC、GLIBCXX 和 Qt 相关依赖。

不要通过强制忽略依赖的方式解决版本不兼容问题。

### 9.5 程序关闭后仍有后台进程

检查：

```bash
pgrep -af 'geekdash|geekdash-net-audit-helper'
```

如果存在异常残留进程，请保存程序日志和系统日志，以便进一步排查。

不要直接使用强制结束 Root Helper 的方式替代正常生命周期清理。

---

## 10. 发行包验证状态

当前 Linux 发行包已经完成以下构建与静态验证：

| 验证项目 | 状态 |
|---|---|
| DEB 构建 | 已通过 |
| RPM 构建 | 已通过 |
| ZIP 构建 | 已通过 |
| SHA256 校验 | 已通过 |
| DEB 内容检查 | 已通过 |
| RPM 内容检查 | 已通过 |
| ZIP CRC 检查 | 已通过 |
| Helper 打包检查 | 已通过 |
| Polkit Policy 打包检查 | 已通过 |
| Desktop Entry 打包检查 | 已通过 |
| 跨发行版实际安装测试 | 待完成 |
| Linux 实际运行验收 | 待完成 |
| 网络审计完整功能验收 | 待完成 |
| 卸载清理验收 | 待完成 |

构建通过不等于所有 Linux 发行版均已完成运行兼容性认证。

---

## 11. 技术信息

当前 Linux 构建使用：

- Python 3.14.4
- PyInstaller 6.22.3
- PySide6 6.12.0
- psutil 7.2.2
- x86_64
- GLIBC 2.43

发行包包括：

- DEB 安装包。
- RPM 安装包。
- ZIP 通用部署包。
- SHA256 校验清单。
- JSON 构建报告。

---

## 12. 安全说明

GeekDash 的系统级功能涉及系统信息读取和网络审计。

请遵循以下原则：

1. 仅从可信来源获取安装包。
2. 安装前验证 SHA256。
3. 不要随意修改 Root Helper 的权限。
4. 不要将 GUI 整体设置为 Root 启动。
5. 不要随意修改 Polkit 授权策略。
6. 不要通过关闭系统安全机制解决授权问题。
7. 仅在拥有授权的设备和网络环境中使用网络审计功能。

---

## 13. 版本信息

**GeekDash Linux Documentation**

文档版本：v1.0.0

当前 Linux 软件包版本：8.0.0

架构：Linux x86_64 / AMD64

发行格式：DEB / RPM / ZIP

EOF

echo "========== README 创建完成 =========="
ls -lh README_LINUX.md

echo
echo "========== 文档行数 =========="
wc -l README_LINUX.md

echo
echo "========== 版本号检查 =========="
grep -nE 'v1\.0\.0|8\.0\.0|GLIBC_2\.43' README_LINUX.md
```

## 二、这份 README 的定位

这不是简单的安装说明，而是 Linux 用户使用文档，包含：

1. 产品介绍。
2. 系统要求。
3. DEB 安装。
4. RPM 安装。
5. ZIP 部署。
6. Root Helper 和 Polkit 权限机制。
7. 程序启动。
8. 卸载。
9. SHA256 验证。
10. 故障排查。
11. 兼容性声明。
12. 安全说明。
