<div align="center">

# 123云盘 第三方 Android 客户端

**基于 Android WebView 壳 + 内嵌 Web 前端 的 123云盘 非官方第三方客户端**

主题切换 · 自定义下载目录 · 屏幕常亮 · 传输管理 · 多账号切换

<br>

[![Platform](https://img.shields.io/badge/platform-Android%207.0%2B-brightgreen.svg)](https://github.com/sillycats/123pan-mobile-app)
[![Language](https://img.shields.io/badge/language-Java%20%2B%20JS-orange.svg)](https://github.com/sillycats/123pan-mobile-app)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Original](https://img.shields.io/badge/original-qq5855144%2F123pan--mobile--app-blue.svg)](https://github.com/qq5855144/123pan-mobile-app)
[![PRs-welcome](https://img.shields.io/badge/PRs-welcome-blueviolet.svg)](https://github.com/sillycats/123pan-mobile-app/pulls)

</div>

---

## 📑 目录

- [📥 下载安装](#-下载安装)
- [📖 项目简介](#-项目简介)
- [✨ 功能特性](#-功能特性)
- [🏗 技术架构](#-技术架构)
- [🔨 本地构建](#-本地构建)
- [🙏 开源项目致谢](#-开源项目致谢)
- [📄 版权与许可证](#-版权与许可证)
- [📋 免责声明](#-免责声明)
- [⭐ 支持本项目](#-支持本项目)

---

## 📥 下载安装

前往 [Releases](https://github.com/sillycats/123pan-mobile-app/releases) 页面下载最新 APK：

- **GitHub Releases**：https://github.com/sillycats/123pan-mobile-app/releases
- **GitHub 仓库**：https://github.com/sillycats/123pan-mobile-app

> 安装时如提示"未知来源"，请在系统设置中允许安装来自此来源的应用。

---

## 📖 项目简介

本项目是 **123云盘** 的第三方 Android 客户端，基于 [qq5855144/123pan-mobile-app](https://github.com/qq5855144/123pan-mobile-app) 二次开发，通过调用 123云盘 公开的 Web API 实现文件浏览、上传下载、分享、回收站等常用功能。

采用 **Android WebView 壳 + 内嵌 Web 前端** 架构：前端使用 `index.html` / `style.css` / `app.js`，通过原生桥调用系统能力（文件选择、下载、屏幕常亮等），网络请求由原生层发起并附加登录态。

> ⚠️ 本项目**与 123云盘官方无任何关联**，并非官方出品。详见 [免责声明](#-免责声明)。

---

## ✨ 功能特性

- **文件管理**：浏览/新建/重命名/删除/移动/复制文件与文件夹，面包屑导航，多视图排序
- **上传下载**：文件/文件夹上传，断点续传，传输任务列表与进度展示，同名文件自动更名保留两者
- **自定义下载目录**：默认 `Download/123云盘/`，支持通过系统目录选择器（SAF）自定义
- **屏幕常亮**：手动开关 + 上传/下载进行中自动保持屏幕常亮，传输结束自动恢复
- **明暗主题**：跟随系统 / 白天 / 夜间三种模式，设置持久化，搜索栏与底部工具栏同步切换
- **多账号管理**：token 本地持久化，切换账号免重新登录
- **分享功能**：创建分享链接、接收分享、我的分享列表
- **回收站**：文件回收站浏览、恢复、彻底删除、清空
- **修改密码**：内置修改密码表单页
- **删除记录选项**：删除已下载文件记录时可选"仅删记录"或"同时删除本地文件"
- **文件预览**：图片/视频/PDF/文本/Office 在线预览（经原生带认证头代理）
- **自动更新**：内置检查更新，从本仓库 Releases 拉取新版 APK

---

## 🏗 技术架构

```
app/src/main/
├── assets/                  # Web 前端（index.html / style.css / app.js）
├── java/com/pan/mobile/     # Android 原生（MainActivity / PanProvider / NativeBridge）
├── res/                     # 图标与主题资源
└── AndroidManifest.xml
scripts/build.sh              # 完整构建 + 签名脚本（aapt2 → javac → d8 → zipalign → apksigner）
```

- **认证**：原生层发起 HTTP 请求并附加 `Authorization: Bearer <token>` 头
- **文件下载**：自研流式下载器，带认证头、多级直链解析与字节校验
- **FileProvider**：`PanProvider` 提供文件共享，用于 APK 安装与打开方式

---

## 🔨 本地构建

依赖：JDK 17 + Android SDK（platform-34 / build-tools-34.0.0）。

```bash
export PATH=/path/to/jdk-17/bin:$PATH
export ANDROID_HOME=/path/to/android-sdk

ANDROID_KEYSTORE=/path/to/your.keystore \
ANDROID_KEYSTORE_PASS=your_password \
ANDROID_KEYSTORE_ALIAS=your_alias \
VERSION_CODE=1088 VERSION_NAME=1.0.88 \
./scripts/build.sh
```

---

## 🙏 开源项目致谢

本项目在以下开源项目基础上修改完善，向原作者致谢：

- **[qq5855144/123pan-mobile-app](https://github.com/qq5855144/123pan-mobile-app)** — 原始 123云盘 WebView 客户端，本项目的核心框架与文件管理逻辑均基于此项目二次开发
- 123云盘 Web API（`api.123pan.cn`）— 所有文件/用户/分享接口的提供方

如有侵权或问题，请联系原作者或本项目维护者删除。

---

## 📄 版权与许可证

- 本项目（sillycats 的修改部分）以 [MIT License](LICENSE) 开源
- 原始项目版权归 [qq5855144](https://github.com/qq5855144) 所有，遵循其原有开源协议
- **"123云盘"**、**"123pan"** 名称、Logo、商标及相关图形版权归 123云盘官方所有
- 本项目仅为学习与研究用途的第三方客户端，**不代表官方立场，也未获得官方授权**

---

## 📋 免责声明

1. 本项目为个人学习与技术研究目的开发的**非官方第三方客户端**，与 123云盘官方及其关联公司**无任何隶属、合作或授权关系**。
2. 本项目通过调用 123云盘公开 Web API 实现功能，使用风险与后果由使用者自行承担。因使用本程序导致的任何直接或间接损失（包括但不限于账号异常、文件丢失、数据泄露、封禁等），作者概不负责。
3. 请在遵守 123云盘用户协议及相关法律法规的前提下使用本软件。**请勿用于任何商业用途或违反服务条款的场景**。
4. 本项目不收集、不上传任何用户的账号密码与文件数据，所有登录凭证与文件均存储于用户本地设备。
5. 若 123云盘官方要求停止分发，本项目将在收到通知后立即下架。

---

## ⭐ 支持本项目

如果觉得本项目对你有帮助，欢迎点个 Star ⭐，或在 [Issues](https://github.com/sillycats/123pan-mobile-app/issues) 反馈问题、提交 PR。
