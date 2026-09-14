# Solie

Solie 是本地多模态创作工作台，提供自由画布、电商套图、视频广告、在线生图、在线对话及图片处理工具。

此仓库仅发布安装包、版本说明和更新信息，不包含产品源码。首个发布版本为 **0.1.0**。

## 下载

前往 [最新版本](https://github.com/Whisper-CN/Solie-releases/releases/latest)，在 Assets 中选择安装包：

| 系统 | 文件 |
| --- | --- |
| macOS · Apple Silicon（M 系列芯片） | `Solie-版本号-mac-arm64.dmg` |
| Windows · x64 | `Solie-版本号-win-x64-Setup.exe` |

当前不提供 Intel Mac 或 Windows ARM 原生安装包。无需额外安装 Node.js、npm 或 FFmpeg；视频广告支持素材导出，不提供成片合成。

**当前安装包未签名，Mac 版也未经过 Apple 公证。首次下载或启动可能被系统拦截，具体提示取决于系统版本与安全策略。** 请仅从本仓库的 Releases 下载。

## macOS 安装

1. 下载 `.dmg` 并双击打开。
2. 将 `Solie.app` 拖到「应用程序」（Applications）文件夹，等待复制完成。
3. 从「应用程序」启动 Solie，不要一直从磁盘映像内运行。

### 提示无法验证开发者或 Apple 无法检查恶意软件

尝试打开后，进入「系统设置 → 隐私与安全性」，找到 Solie 被阻止的记录，点击「仍要打开」，按系统提示确认。仅在确认文件来自本仓库且信任发布者后操作。参见 [Apple 官方说明](https://support.apple.com/zh-cn/102445)。

### 提示“Solie 已损坏，无法打开”

这个提示不能直接证明只是未签名，也可能是下载不完整或文件被修改。请先重新下载，并核对当前 Release 中的 SHA-256 校验值。Mac 终端示例（按实际下载位置调整）：

```sh
shasum -a 256 ~/Downloads/Solie-0.1.0-mac-arm64.dmg
```

确认校验值一致、应用来自本仓库，且已复制到「应用程序」后，如果仍因下载隔离标记无法启动，可自行在终端对 **Solie 这一个应用** 移除该标记，再打开：

```sh
xattr -dr com.apple.quarantine /Applications/Solie.app
```

此命令会移除 Solie 的下载隔离属性，使该副本不再受这项下载隔离检查；不会为软件补上签名、公证或修复真正损坏的文件。若提示权限不足，不要对整个应用程序目录执行命令；请检查安装位置与文件权限。若仍无法启动，或系统明确提示恶意软件/将损害电脑，请停止尝试并在 [Issues](https://github.com/Whisper-CN/Solie-releases/issues) 反馈提示内容和系统版本。不要关闭系统级 Gatekeeper 或杀毒保护。

## Windows 安装

1. 下载 `Solie-版本号-win-x64-Setup.exe`。
2. 双击运行，按安装向导选择路径并完成安装。
3. 从桌面快捷方式或开始菜单打开 Solie。

如果出现「Windows 已保护你的电脑」或“未知发布者”，确认安装包来自本仓库且校验值一致后，可在系统提供该选项时点击「更多信息 → 仍要运行」。某些组织策略或 Smart App Control 可能不提供继续入口；不要为安装而关闭全局保护。参见 [Microsoft 关于应用信誉与拦截的说明](https://learn.microsoft.com/en-us/windows/apps/package-and-deploy/smartscreen-reputation)。

PowerShell 校验示例：

```powershell
Get-FileHash "$env:USERPROFILE\Downloads\Solie-0.1.0-win-x64-Setup.exe" -Algorithm SHA256
```

## 首次使用与本地数据

打开后在应用设置中配置自己的 API Key。安装包不包含开发者的 Key 或 `.env`，AI 功能需要可用网络和有效的服务配置。

- Mac 数据目录：`~/Library/Application Support/Solie/`
- Windows 数据目录：`%APPDATA%\Solie\`

项目与素材保存在 `Projects`，运行数据与日志在 `Runtime`，连接器配置在 `Config`；API Key 与路由设置通过系统加密后保存为 `credentials.bin`。数据不会自动在两台电脑间同步。

## 更新

从 **0.1.0** 起，可在「设置 → 关于 → 检查更新」查看新版本并打开对应安装包链接。当前采用手动下载安装，不自动安装或重启。

更新前等待生成任务结束、保存项目并完全退出 Solie，再覆盖安装新版。Mac 使用菜单「退出 Solie」；Windows 关闭最后一个窗口即退出。正常覆盖安装保留项目和设置，建议更新前备份本地数据，勿删除数据目录。此前测试包即使同为 0.1.0，也需手动替换为本次发布的安装包。
