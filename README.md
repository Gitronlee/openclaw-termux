# OpenClaw

[![下载 APK](https://img.shields.io/badge/下载-APK-green?style=for-the-badge&logo=android)](https://github.com/Gitronlee/openclaw-termux/releases/latest)
[![构建 Flutter APK & AAB](https://github.com/Gitronlee/openclaw-termux/actions/workflows/flutter-build.yml/badge.svg)](https://github.com/Gitronlee/openclaw-termux/actions/workflows/flutter-build.yml)
[![npm 版本](https://img.shields.io/npm/v/openclaw-termux?color=blue&label=npm)](https://www.npmjs.com/package/openclaw-termux)
[![许可证: MIT](https://img.shields.io/badge/许可证-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js](https://img.shields.io/badge/Node.js-22-green?logo=node.js)](https://nodejs.org/)
[![Android](https://img.shields.io/badge/Android-10%2B-brightgreen?logo=android)](https://www.android.com/)
[![Flutter](https://img.shields.io/badge/Flutter-3.24-02569B?logo=flutter)](https://flutter.dev/)
[![欢迎提交 PR](https://img.shields.io/badge/PR-欢迎-brightgreen.svg)](https://github.com/Gitronlee/openclaw-termux/pulls)

<p align="center">
  <img src="assets/ic_launcher.png" alt="OpenClaw 应用预览" width="700"/>
</p>

> 在 Android 上运行 **OpenClaw AI 网关** — 独立的 Flutter 应用，内置终端、Web 仪表板、可选的开发工具，一键设置。也可作为 Termux CLI 包使用。

---

## 截图

<table align="center">
  <tr>
    <td align="center"><img src="assets/dashboard.png" alt="仪表板" width="220"/><br/><b>仪表板</b></td>
    <td align="center"><img src="assets/setupscreen.png" alt="设置" width="220"/><br/><b>设置向导</b></td>
    <td align="center"><img src="assets/onboardingscreen.png" alt="引导" width="220"/><br/><b>引导</b></td>
  </tr>
  <tr>
    <td align="center"><img src="assets/websscreen.png" alt="Web 仪表板" width="220"/><br/><b>Web 仪表板</b></td>
    <td align="center"><img src="assets/logscreen.png" alt="日志" width="220"/><br/><b>日志</b></td>
    <td align="center"><img src="assets/settingsscreen.png" alt="设置" width="220"/><br/><b>设置</b></td>
  </tr>
</table>

---

## 什么是 OpenClaw？

OpenClaw 将 [OpenClaw](https://github.com/anthropics/openclaw) AI 网关带到 Android。它通过 proot 设置完整的 Ubuntu 环境，安装 Node.js 和 OpenClaw，并提供原生 Flutter UI 来管理所有内容 — 无需 root 权限。

### 两种使用方式

| | **Flutter 应用**（独立） | **Termux CLI** |
|---|---|---|
| 安装 | 构建 APK 或下载发布版本 | `npm install -g openclaw-termux` |
| 设置 | 点击「开始设置」 | `openclawx setup` |
| 网关 | 点击「启动网关」 | `openclawx start` |
| 终端 | 内置终端模拟器 | Termux shell |
| 仪表板 | 内置 WebView | 浏览器访问 `localhost:18789` |

---

## 功能特性

### Flutter 应用
- **一键设置** — 自动下载 Ubuntu rootfs、Node.js 22 和 OpenClaw
- **内置终端** — 完整的终端模拟器，带额外按键工具栏、复制/粘贴、可点击的 URL
- **网关控制** — 启动/停止网关，带状态指示器和健康检查
- **AI 提供商** — 为 15 个提供商配置 API 密钥和选择模型，包括 8 个中文模型（Anthropic、OpenAI、Google Gemini、OpenRouter、NVIDIA NIM、DeepSeek、xAI、智谱 GLM、百度文心、通义千问、Moonshot（Kimi）、讯飞星火、MiniMax、百川、零一万物）
- **SSH 远程访问** — 启动/停止 SSH 服务器，设置 root 密码，查看连接信息和可复制命令
- **配置菜单** — 在内置终端中运行 `openclaw configure` 来管理网关设置
- **节点设备功能** — 通过 WebSocket 节点协议向 AI 暴露 7 个功能（15 个命令）
- **Token URL 显示** — 从引导中捕获认证 token，显示带复制按钮
- **Web 仪表板** — 嵌入式 WebView 加载带有认证 token 的仪表板
- **查看日志** — 实时网关日志查看器，带搜索/过滤功能
- **引导** — 直接在应用中配置 API 密钥和绑定
- **可选包** - 安装 Go (Golang)、Homebrew 和 OpenSSH 作为可选开发工具
- **设置** — 自动启动、电池优化、系统信息、包状态、重新运行设置
- **前台服务** — 保持网关在后台运行，带正常运行时间跟踪
- **设置通知** — 环境设置期间带有进度条的通知

### 可选包

初始设置完成后，您可以直接从应用中选择安装开发工具：

| 包 | 安装方法 | 大小 |
|---------|---------------|------|
| **Go (Golang)** | `apt install golang` | ~150 MB |
| **Homebrew** | 官方安装程序（带 root 变通方法） | ~500 MB |
| **OpenSSH** | `apt install openssh-server` | ~10 MB |

这些可以从以下位置访问：
- **设置向导** — 设置完成后出现包卡片
- **仪表板** — 快速操作中的「包」卡片
- **设置** — 在系统信息下显示安装状态

### 节点设备功能

Flutter 应用作为**节点**连接到网关，向 AI 暴露 Android 硬件。启用节点时会主动请求权限。

| 功能 | 命令 | 权限 |
|------------|----------|------------|
| **相机** | `camera.snap`, `camera.clip`, `camera.list` | 相机 |
| **画布** | `canvas.navigate`, `canvas.eval`, `canvas.snapshot` | 无（未实现） |
| **闪光灯** | `flash.on`, `flash.off`, `flash.toggle`, `flash.status` | 相机（手电筒） |
| **位置** | `location.get` | 位置 |
| **屏幕** | `screen.record` | MediaProject 同意 |
| **传感器** | `sensor.read`, `sensor.list` | 身体传感器 |
| **触觉** | `haptic.vibrate` | 无 |

网关的 `openclaw.json` 会在启动前自动打补丁，以清除 `denyCommands` 并为所有 15 个命令设置 `allowCommands`。

### Termux CLI
- **一键设置** — 安装 proot-distro、Ubuntu、Node.js 22 和 OpenClaw
- **Bionic 旁路** — 修复 Android 的 Bionic libc 上的 `os.networkInterfaces()` 崩溃
- **智能加载** — 显示旋转加载器直到网关就绪
- **透传命令** — 通过 `openclawx` 运行任何 OpenClaw 命令

---

## 重要警告

> **存储权限** — 此应用**不需要**完整的存储访问即可运行。如果提示，**拒绝**存储权限，除非您特别需要 proot 访问 `/sdcard`。授予权限后，`MANAGE_EXTERNAL_STORAGE` 允许 proot 环境读取和修改设备上的**所有文件**，包括照片、下载和文档。以前的版本在启动时自动请求此权限，这可能导致意外数据丢失（参见 [#67](https://github.com/mithun50/openclaw-termux/issues/67)、[#63](https://github.com/mithun50/openclaw-termux/issues/63)）。这已修复 — 存储访问现在只能从设置中选择。

> **电池优化** — 在 Android 设置中禁用应用的电池优化，以防止 Android 在后台杀死网关进程。没有这个，网关可能会在几分钟后静默崩溃。

> **首次启动** — 初始设置下载约 500MB（Ubuntu rootfs + Node.js）。在开始之前，请确保您有稳定的互联网连接和足够的存储空间。

---

## 快速开始

### Flutter 应用（推荐）

1. 从「[发布版本](https://github.com/Gitronlee/openclaw-termux/releases)」下载最新的 APK
2. 在您的 Android 设备上安装 APK
3. 打开应用并点击**「开始设置」**
4. 设置完成后，从包卡片中选择安装 **Go** 或 **Homebrew**
5. 在**「引导」**中配置您的 API 密钥
6. 在仪表板上点击**「启动网关」**

或从源代码构建：

```bash
git clone https://github.com/Gitronlee/openclaw-termux.git
cd openclaw-termux/flutter_app
flutter build apk --release
```

### Termux CLI

#### 一行命令（推荐）

```bash
curl -fsSL https://ghp.ci/https://raw.githubusercontent.com/Gitronlee/openclaw-termux/cn/install.sh | bash
```

#### 或通过 npm

```bash
npm install -g openclaw-termux
openclawx setup
```

---

## 系统要求

| 要求 | 详情 |
|-------------|---------|
| **Android** | 10 或更高版本（API 29） |
| **存储** | 约 500MB 用于 Ubuntu + Node.js + OpenClaw |
| **架构** | arm64-v8a、armeabi-v7a、x86_64 |
| **Termux**（仅 CLI） | 从 [F-Droid](https://f-droid.org/packages/com.termux/)（非 Play Store）|

---

## CLI 使用

```bash
# 首次设置（安装 proot + Ubuntu + Node.js + OpenClaw）
openclawx setup

# 检查安装状态
openclawx status

# 启动 OpenClaw 网关
openclawx start

# 运行引导以配置 API 密钥
openclawx onboarding

# 进入 Ubuntu shell
openclawx shell

# 任何 OpenClaw 命令都可以直接运行
openclawx doctor
openclawx gateway --verbose
```

---

## 架构

```
┌───────────────────────────────────────────────────┐
│                Flutter 应用（Dart）               │
│  ┌──────────┐ ┌──────────┐ ┌──────────────┐       │
│  │ 终端     │ │ 网关     │ │ Web 仪表板   │       │
│  │ 模拟器   │ │ 控制器   │ │   (WebView)  │       │
│  └─────┬────┘ └─────┬────┘ └──────┬───────┘       │
│        │            │             │               │
│  ┌─────┴────────────┴─────────────┴─────────────┐ │
│  │           原生桥接（Kotlin）                │ │
│  └─────────────────┬────────────────────────────┘ │
│                    │                              │
│  ┌─────────────────┴────────────────────────────┐ │
│  │         节点提供商（WebSocket）             │ │
│  │  相机 · 闪光灯 · 位置 · 屏幕                │ │
│  │  传感器 · 触觉 · 画布                        │ │
│  └─────────────────┬────────────────────────────┘ │
└────────────────────┼──────────────────────────────┘
                     │
┌────────────────────┼──────────────────────────────┐
│  proot-distro      │              Ubuntu          │
│  ┌─────────────────┴──────────────────────────┐   │
│  │   Node.js 22 + Bionic 旁路                │   │
│  │   ┌─────────────────────────────────────┐  │   │
│  │   │  OpenClaw AI 网关                  │  │   │
│  │   │  http://localhost:18789             │  │   │
│  │   │  ← 节点 WS：15 个设备命令          │  │   │
│  │   └─────────────────────────────────────┘  │   │
│  │   可选：Go、Homebrew                       │   │
│  └────────────────────────────────────────────┘   │
└───────────────────────────────────────────────────┘
```

### Flutter 应用结构

```
flutter_app/lib/
├── main.dart                  # 应用入口点
├── constants.dart             # 应用常量、URL 、作者信息
├── models/
│   ├── gateway_state.dart     # 网关状态、日志、token URL
│   ├── node_state.dart        # 节点连接状态
│   ├── node_frame.dart        # WebSocket 帧模型（请求/响应/事件）
│   ├── setup_state.dart       # 设置向导进度
│   ├── optional_package.dart  # 可选包元数据（Go、Homebrew）
│   └── ai_provider.dart       # AI 提供商数据模型（15 个提供商，包括 8 个中文）
├── providers/
│   ├── gateway_provider.dart  # 网关状态管理
│   ├── node_provider.dart     # 节点功能 + 权限管理
│   └── setup_provider.dart    # 设置状态管理
├── screens/
│   ├── splash_screen.dart     # 带路由的启动屏幕
│   ├── setup_wizard_screen.dart    # 首次设置 + 可选包
│   ├── onboarding_screen.dart      # API 密钥配置终端
│   ├── dashboard_screen.dart       # 带快速操作的主仪表板
│   ├── terminal_screen.dart        # 完整终端模拟器
│   ├── configure_screen.dart       # openclaw configure 终端
│   ├── web_dashboard_screen.dart   # OpenClaw 仪表板的 WebView
│   ├── providers_screen.dart       # AI 提供商列表
│   ├── provider_detail_screen.dart # API 密钥 + 模型配置
│   ├── ssh_screen.dart             # SSH 服务器管理
│   ├── packages_screen.dart        # 可选包管理器
│   ├── package_install_screen.dart # 基于终端的包安装程序
│   ├── logs_screen.dart            # 网关日志查看器
│   └── settings_screen.dart        # 应用设置和关于
├── services/
│   ├── native_bridge.dart     # Kotlin 平台通道桥接
│   ├── gateway_service.dart   # 网关生命周期、健康检查、配置打补丁
│   ├── node_service.dart      # 节点 WebSocket 连接 + 调用处理
│   ├── node_ws_service.dart   # 原始 WebSocket 传输
│   ├── node_identity_service.dart # 设备身份 + 加密签名
│   ├── terminal_service.dart  # proot shell 配置
│   ├── bootstrap_service.dart # 环境设置编排
│   ├── package_service.dart   # 可选包状态检查
│   ├── preferences_service.dart # 持久化设置（token URL 等）
│   ├── provider_config_service.dart # AI 提供商配置读/写
│   ├── ssh_service.dart       # 通过原生桥接管理 SSH 服务器
│   └── capabilities/
│       ├── capability_handler.dart   # 带权限处理的基类
│       ├── camera_capability.dart    # 照片/视频捕获
│       ├── canvas_capability.dart    # WebView 存根（未实现）
│       ├── flash_capability.dart     # 手电筒 开/关/切换
│       ├── location_capability.dart  # 带超时 + 回退的 GPS
│       ├── screen_capability.dart    # 通过 MediaProject 的屏幕录制
│       ├── sensor_capability.dart    # 加速度计、陀螺仪等
│       └── vibration_capability.dart # 触觉反馈
└── widgets/
    ├── gateway_controls.dart  # 启动/停止、URL 显示、复制按钮
    ├── node_controls.dart     # 节点启用/禁用、状态徽章
    ├── terminal_toolbar.dart  # 额外按键（Tab、Ctrl、Esc、箭头）
    ├── status_card.dart       # 可重用的状态卡片
    └── progress_step.dart     # 设置向导步骤指示器
```

---

## 配置

### 引导

运行引导时（在应用内或通过 `openclawx onboarding`）：

- **绑定**：对于非 root 设备，选择 `Loopback (127.0.0.1)`
- **API 密钥**：添加您的 Gemini/OpenAI/Claude 密钥
- **Token URL**：应用自动捕获并存储认证 token URL（例如 `http://localhost:18789/#token=...`）

### 电池优化

> **重要**：禁用应用的电池优化以保持网关在后台运行。

**对于 Flutter 应用**：设置 > 电池优化 > 点击以禁用

**对于 Termux**：Android 设置 > 应用 > Termux > 电池 > **不受限制**

---

## 仪表板

在应用中显示的 token URL 访问 Web 仪表板（例如 `http://localhost:18789/#token=...`）。

Flutter 应用通过内置 WebView 自动加载带有您的认证 token 的仪表板。

| 命令 | 描述 |
|---------|-------------|
| `/status` | 检查网关状态 |
| `/think high` | 启用高质量思考 |
| `/reset` | 重置会话 |

---

## 故障排除

### 使用应用后文件被删除或丢失

v1.8.4 之前的版本在启动时自动请求完整的存储访问（`MANAGE_EXTERNAL_STORAGE`）。结合 proot rootfs 内指向 `/sdcard` 的符号链接，清理操作可能会跟随这些符号链接并删除真实的用户文件。**这已修复** — 不再自动请求存储权限，删除时不跟随符号链接，并且路径边界检查可防止应用私有目录外的任何删除。如果您受到影响，请参见 [#67](https://github.com/mithun50/openclaw-termux/issues/67)。

要撤销存储权限：Android 设置 > 应用 > OpenClaw > 权限 > 文件和媒体 > 不允许。

### 网关无法启动

```bash
# 检查状态
openclawx status

# 如需要，重新运行设置
openclawx setup

# 确保引导已完成
openclawx onboarding
```

### "os.networkInterfaces" 错误

未配置 Bionic 旁路。再次运行设置：

```bash
openclawx setup
```

### 进程在后台被杀死

在 Android 设置中禁用应用的电池优化。

### 权限被拒绝

```bash
termux-setup-storage
```

---

## 手动设置

<details>
<summary>点击展开手动安装步骤</summary>

### 1. 安装 proot-distro 和 Ubuntu

```bash
pkg update && pkg install -y proot-distro
proot-distro install ubuntu
```

### 2. 在 Ubuntu 中设置 Node.js

```bash
proot-distro login ubuntu
apt update && apt install -y curl
curl -fsSL https://deb.nodesource.com/setup_22.x | bash -
apt install -y nodejs
npm install -g openclaw
```

### 3. 创建 Bionic 旁路

```bash
mkdir -p ~/.openclaw
cat > ~/.openclaw/bionic-bypass.js << 'EOF'
const os = require('os');
const originalNetworkInterfaces = os.networkInterfaces;
os.networkInterfaces = function() {
  try {
    const interfaces = originalNetworkInterfaces.call(os);
    if (interfaces && Object.keys(interfaces).length > 0) {
      return interfaces;
    }
  } catch (e) {}
  return {
    lo: [{
      address: '127.0.0.1',
      netmask: '255.0.0.0',
      family: 'IPv4',
      mac: '00:00:00:00:00:00',
      internal: true,
      cidr: '127.0.0.1/8'
    }]
  };
};
EOF
```

### 4. 添加到 bashrc

```bash
echo 'export NODE_OPTIONS="--require ~/.openclaw/bionic-bypass.js"' >> ~/.bashrc
source ~/.bashrc
```

### 5. 运行 OpenClaw

```bash
openclaw onboarding  # 选择 "Loopback (127.0.0.1)"
openclaw gateway --verbose
```

</details>

---

## 贡献

欢迎贡献！请随时提交 Pull Request。

1. Fork 仓库
2. 创建您的功能分支（`git checkout -b feature/amazing-feature`）
3. 提交您的更改（`git commit -m 'Add amazing feature'`）
4. 推送到分支（`git push origin feature/amazing-feature`）
5. 打开 Pull Request

---

## 作者

**Mithun Gowda B** | [NextGenX](https://play.google.com/store/apps/dev?id=8262374975871504599)

- GitHub: [@mithun50](https://github.com/mithun50)
- Email: [mithungowda.b7411@gmail.com](mailto:mithungowda.b7411@gmail.com)
- Instagram: [@nexgenxplorer_nxg](https://www.instagram.com/nexgenxplorer_nxg)
- YouTube: [@nexgenxplorer](https://youtube.com/@nexgenxplorer?si=UG-wBC8UIyeT4bbw)
- Play Store: [NextGenX Apps](https://play.google.com/store/apps/dev?id=8262374975871504599)
- 联系方式: [nxgextra@gmail.com](mailto:nxgextra@gmail.com)

## 国内镜像分支维护者

**Gitronlee** 

- GitHub: [@Gitronlee](https://github.com/Gitronlee)

---

## 许可证

MIT 许可证 - 详见 [LICENSE](LICENSE) 文件。

---
## ⭐ Star 历史

[![Star 历史图表](https://api.star-history.com/svg?repos=Gitronlee/openclaw-termux&type=Date)](https://star-history.com/#Gitronlee/openclaw-termux&Date)


<p align="center">
  为 Android 社区用 &#10084;&#65039; 制作，作者 <a href="https://github.com/mithun50">Mithun Gowda B</a> | <b>NextGenX</b>
  <br>
  国内镜像分支维护：<a href="https://github.com/Gitronlee">Gitronlee</a>
</p>
