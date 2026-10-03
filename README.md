# wickrunAI（灯芯AI）安装包

这里发布 wickrunAI 的官方安装包。应用内的自动更新和 [wickrunai.com/download](https://wickrunai.com/download) 都从这里获取文件。

**[下载最新版本 →](https://github.com/lifishard/wickrunAI-releases/releases/latest)**

| 系统 | 选哪个文件 |
| --- | --- |
| Windows | `…-win-x64-setup.exe`（安装版，可自动更新）；免安装用 `…-win-x64-portable.exe` |
| macOS | Apple 芯片选 `…-mac-arm64.dmg`，Intel 选 `…-mac-x64.dmg` |
| Linux | `…-linux-x64.AppImage`（可自动更新）或 `…-linux-x64.deb` |
| Android | `…-android-preview.apk`（预览版；从 3.x 升级前请先看版本说明里的备份提醒） |

每个版本的说明写在对应的 Release 页面上。以 `.yml` 和 `.blockmap` 结尾的文件供自动更新使用，不需要手动下载。

安装包目前没有代码签名：Windows SmartScreen 和 macOS Gatekeeper 会提示“未知发布者”，这是预期行为。只从本页或 wickrunai.com 下载。

## 反馈

问题和建议请提交到 [Issues](https://github.com/lifishard/wickrunAI-releases/issues)，写明应用版本、系统和复现步骤，附日志前请删除 API 密钥和私人内容。安全问题请发邮件到 admin@wickrunai.com，不要公开贴出细节。

## 许可

wickrunAI 4.1.1 及以后的版本为专有软件，按 [wickrunAI 软件许可](LICENSE) 免费使用；本仓库只提供安装包，不包含源代码。4.1.0 及更早版本以 Apache License 2.0 发布。应用中使用的开源组件按各自许可证授权，清单随应用提供（`THIRD_PARTY_LICENSES.txt`）。

---

# wickrunAI installers

Official installers for wickrunAI. In-app updates and [wickrunai.com/download](https://wickrunai.com/download) read from this repository. **[Download the latest version →](https://github.com/lifishard/wickrunAI-releases/releases/latest)**

Pick `-win-x64-setup.exe` (Windows), `-mac-arm64.dmg` or `-mac-x64.dmg` (macOS), `-linux-x64.AppImage` or `.deb` (Linux), or `-android-preview.apk` (Android preview). The `.yml` and `.blockmap` files are for automatic updates. Installers are not code-signed yet, so Windows and macOS warn about an unknown publisher; download only from here or wickrunai.com.

Report problems in [Issues](https://github.com/lifishard/wickrunAI-releases/issues); report security issues privately to admin@wickrunai.com.

wickrunAI 4.1.1 and later are proprietary software, free to use under the [wickrunAI Software License](LICENSE). This repository contains installers only, not source code. Versions 4.1.0 and earlier were released under the Apache License 2.0. Open-source components keep their own licenses, listed in `THIRD_PARTY_LICENSES.txt` inside the app.
