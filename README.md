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
- [🔧 相比原版新增与修改](#-相比原版新增与修改)
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
- **离线下载**：传输页新增离线下载 Tab，支持磁力链接 / HTTP(S) 直链解析并提交到云端离线下载
- **相册视图**：文件页工具栏新增相册按钮，6 路并发 BFS 遍历全盘图片/视频，网格缩略图展示，点击预览
- **删除记录选项**：删除已下载文件记录时可选"仅删记录"或"同时删除本地文件"
- **文件预览**：图片/视频/PDF/文本/Office 在线预览（经原生带认证头代理）
- **自动更新**：内置检查更新，从本仓库 Releases 拉取新版 APK

---

## 🔧 相比原版（qq5855144）新增与修改

以下为在原开源项目基础上新增、修复或调整的内容：

### 🆕 新增功能

- **主题模式**：跟随系统 / 白天 / 夜间三种模式，CSS 变量化实现，设置持久化；修复了跟随系统未生效、夜间模式下搜索栏与底部工具栏未变色的问题
- **自定义下载目录**：默认 `/storage/emulated/0/Download/123云盘/`，支持通过系统 SAF 目录选择器自由选择
- **屏幕常亮**：设置页手动开关；上传/下载进行中自动保持屏幕常亮，传输结束自动恢复正常熄屏
- **删除记录选项**：删除已完成的文件传输记录时，弹窗可选"仅删除记录"或"同时删除本地文件"
- **修改密码表单页**：独立的表单式修改密码界面（旧密码/新密码/确认新密码），前端校验
- **设置页分类规范**：按"账号管理 / 存储 / 分享 / 偏好设置"分组排序
- **滚动位置记忆**：切换底部 Tab（文件/传输/回收站/我的）后再切回文件页，列表滚动位置保持不变
- **离线下载**：传输页新增"离线下载"标签，输入磁力链接或 HTTP(S) 直链，自动调解析接口 → 提交接口，云端离线下载完成后文件出现在网盘根目录
- **相册视图**：文件页工具栏新增"相册"按钮，6 路并发 BFS 递归遍历全盘目录，收集图片/视频并以 3 列网格缩略图展示，底部叠加文件名，点击直接预览
- **相册缩略图**：新增原生 bridge `getThumbnail` 接口，调 123pan 缩略图 API 加载真实缩略图（base64 返回）

### 🐛 修复问题

- **首页文件不显示**：修复文件列表接口解析，文件夹与文件正常展示
- **低版本闪退**：从 WebView 壳改为 Java 源码编译，规避 smali 手写修改与 `MediaStore$Downloads` 类加载导致的闪退
- **返回键需按两次**：修复进入文件夹后按返回键不回退目录的 bug（pop 后 currentDir 被错误设回当前目录 id）
- **文件详细信息弹窗**：修复 HTML 被当纯文本显示的问题，改为 innerHTML 渲染
- **同名文件处理**：默认改为"自动更名保留两者"，不再每次弹窗询问
- **文件夹点击交互**：单击文件夹直接进入查看文件，长按文件夹弹出操作菜单（分享/详细信息/重命名/删除）；文件单击/长按均弹出操作菜单

### 🗑 移除/调整

- 移除了原个人信息页中的头像/昵称/手机号/邮箱/实名认证等未完整对接的项，修改密码接口手机端不开放已删除
- 移除了收藏、直链、收藏管理入口（对应接口在手机端未开放，点击会报 no Route matched）
- 移除了设置页中"同名文件处理"入口（默认策略已固定为保留两者）
- 自动更新源切换为当前仓库 `sillycats/123pan-mobile-app` 的 Releases

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
