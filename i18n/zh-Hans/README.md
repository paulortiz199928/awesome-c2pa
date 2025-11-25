# Awesome C2PA [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> C2PA（内容来源和真实性联盟）资源精选列表，包括多语言规范、工具、库和学习材料。

**[English](../../README.md) | 简体中文 | [繁體中文](../zh-Hant/README.md) | [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Deutsch](../de/README.md) | [Français](../fr/README.md) | [Русский](../ru/README.md)**

C2PA 是一个开放的技术标准，为发布者、创作者和消费者提供追溯不同类型媒体来源的能力。在 AI 生成内容的时代，C2PA 帮助验证内容的真实性和来源。

## 🌟 亮点

**🌍 多语言官方规范** - 本项目提供了首个社区驱动的 C2PA 官方规范多语言翻译，让全球开发者都能使用 C2PA。

**🤝 帮助改进翻译** - 我们的翻译由 AI 辅助（DeepL）且处于测试阶段。母语者：[报告错误](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md) 帮助提高质量！

## 目录

- [官方规范（多语言）](#-官方规范多语言)
- [什么是 C2PA？](#-什么是-c2pa)
- [常见问题](#-常见问题)
- [官方资源](#-官方资源)
- [工具和库](#-工具和库)
  - [Rust](#rust)
  - [JavaScript/TypeScript](#javascripttypescript)
  - [Python](#python)
  - [Go](#go)
  - [Java](#java)
  - [其他语言](#其他语言)
- [命令行工具](#-命令行工具)
- [浏览器扩展和应用](#-应用)
- [学习资源](#-学习资源)
  - [教程](#教程)
  - [视频](#视频)
  - [文章和博客](#文章和博客)
- [用例和演示](#-用例和演示)
- [组织和生态系统](#-组织和生态系统)
- [新闻和更新](#-新闻和更新)
- [社区](#-社区)
- [贡献](#-贡献)
- [许可证](#-许可证)

---

## 🌍 官方规范（多语言）

C2PA 规范 2.2 版本提供多语言版本。这些翻译帮助全球开发者理解和在其应用中实现 C2PA。

| 语言 | 文档 | 状态 | 方法 | 最后更新 |
|----------|----------|--------|--------|--------------|
| 🇬🇧 英语 | [C2PA 规范 2.2](../../docs/specifications/C2PA_Specification.pdf) | ✅ 官方版本 | C2PA 组织 | 2025年5月 |
| 🇨🇳 简体中文 | [C2PA 规范 2.2](../../docs/specifications/C2PA_Specification_zh-Hans.pdf) | 🔄 测试版 | AI + 审核 | 2025 |
| 🇯🇵 日本語 | [C2PA 仕様 2.2](../../docs/specifications/C2PA_Specification_ja.pdf) | 🔄 测试版 | AI + 审核 | 2025 |
| 🇩🇪 Deutsch | [C2PA Spezifikation 2.2](../../docs/specifications/C2PA_Specification_de.pdf) | 🔄 测试版 | AI + 审核 | 2025 |
| 🇫🇷 Français | [Spécification C2PA 2.2](../../docs/specifications/C2PA_Specification_fr.pdf) | 🔄 测试版 | AI + 审核 | 2025 |
| 🇰🇷 한국어 | 即将推出 | 🚧 计划中 | - | - |
| 🇪🇸 Español | 即将推出 | 🚧 计划中 | - | - |
| 🇵🇹 Português | 即将推出 | 🚧 计划中 | - | - |

> **翻译说明**：非英语翻译由 AI 辅助（DeepL）并经过社区审核。虽然我们力求准确，但可能存在错误。鼓励母语者[报告问题](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md)或提交更正。英文版本仍是权威参考。

**快速导航**：[查看所有规范 →](../../docs/README.md)

---

## 🤔 什么是 C2PA？

**C2PA（内容来源和真实性联盟）** 是一个开放标准，为媒体文件添加加密签名的元数据，实现内容来源和编辑历史的验证。

**主要优势：**
- ✅ 验证内容真实性并检测篡改
- ✅ 跟踪从原始版本到当前版本的完整编辑历史
- ✅ 识别 AI 生成或 AI 修改的内容
- ✅ 保护创作者署名和知识产权

**想深入了解？**
- 📖 [5分钟快速入门指南](quick-start.md) - 立即动手实践
- ❓ [完整常见问题](faq.md) - 25+ 个详细问题解答
- 📚 [技术规范](../../docs/README.md) - 深入了解标准

---

## ❓ 常见问题

快速解答最常见的问题：

<details>
<summary><b>什么是 C2PA，它如何工作？</b></summary>

C2PA 为媒体文件添加加密签名的元数据（"清单"），包含来源信息。任何篡改都会破坏签名，使修改可被检测。它使用标准 PKI（如 HTTPS 证书），而非区块链。
</details>

<details>
<summary><b>C2PA 可以被移除吗？它能检测 AI 生成的图像吗？</b></summary>

**移除**：可以，这是设计使然。C2PA 在*存在时*证明真实性，而不是防止移除。

**AI 检测**：不能自动检测。C2PA 记录创作者声明的内容。AI 工具必须自愿在清单中标记其输出为"AI 生成"。
</details>

<details>
<summary><b>哪些相机和软件支持 C2PA？</b></summary>

**相机**：Leica（M11-P、SL3）、Sony（Alpha 1、A9 III、A7S III、A7 IV）、Nikon（Z6 III 计划于 2025 年支持）可在拍摄时签名照片。

**软件**：Adobe Photoshop/Lightroom、Capture One 和许多开源工具。

**成本**：标准和工具免费。证书费用：约 50-500 美元/年。
</details>

**[→ 查看全部 25+ 个常见问题](faq.md)** 涵盖技术细节、隐私、安全和采用情况。

---

## 📚 官方资源

- [C2PA 官方网站](https://c2pa.org/) - 主网站，包含新闻和信息
- [C2PA 规范](https://c2pa.org/specifications/specifications/2.2/index.html) - 官方规范门户（v2.2）
- [C2PA GitHub 组织](https://github.com/c2pa-org) - 官方 GitHub 仓库
- [内容真实性倡议](https://contentauthenticity.org/) - Adobe 领导的支持 C2PA 的倡议

---

## 🛠️ 工具和库

### Rust

- [c2pa-rs](https://github.com/contentauth/c2pa-rs) - 用于创建和验证 C2PA 清单的官方 Rust SDK。参考实现。

### JavaScript/TypeScript

- [c2pa-node-v2](https://github.com/contentauth/c2pa-node-v2) - C2PA Rust SDK 的官方 Node.js 绑定
- [c2pa-js](https://github.com/contentauth/c2pa-js) - 在浏览器中读取 C2PA 清单的 JavaScript 库

### Python

- [c2pa-python](https://github.com/contentauth/c2pa-python) - C2PA Rust SDK 的官方 Python 绑定

### Java

- [c2pa-java](https://github.com/contentauth/c2pa-java) - C2PA SDK 的 Java 绑定

### 其他语言

- [c2pa-c](https://github.com/contentauth/c2pa-c) - C2PA 的 C 和 C++ 绑定
- [c2pa-ios](https://github.com/contentauth/c2pa-ios) - iOS 的 C2PA SDK
- 语言绑定正在扩展 - 查看[官方 GitHub](https://github.com/contentauth/) 获取更新

---

## 🔧 命令行工具

- [C2PA 命令行工具](https://github.com/contentauth/c2pa-rs/tree/main/cli) - 用于创建和检查 C2PA 清单的官方命令行工具
  - 创建、读取和验证 C2PA 内容
  - 跨平台：Windows、macOS、Linux
  - 支持图像、视频、音频

---

## 🌐 应用

- [内容凭证验证](https://contentcredentials.org/verify) - 用于验证 C2PA 内容的官方 Web 工具

---

## 📖 学习资源

### 教程

- [C2PA 快速入门指南](quick-start.md) - C2PA 实现的 5 分钟介绍
- [C2PA 开发者文档](https://opensource.contentauthenticity.org/docs) - 官方入门指南和文档
- [C2PA 开发者教程](https://opensource.contentauthenticity.org/docs/getting-started) - 分步实现教程

### 视频

- [内容真实性倡议介绍](https://www.youtube.com/@contentauthenticity) - 官方 YouTube 频道，包含教育视频
- [C2PA 技术概述](https://www.youtube.com/results?search_query=c2pa+technical) - 会议演讲和技术演示
- [内容凭证如何工作](https://contentauthenticity.org/how-it-works) - C2PA 实际应用的可视化解释

### 文章和博客

- [C2PA 官方网站](https://c2pa.org) - 新闻、更新和技术资源
- [Adobe 内容真实性博客](https://blog.adobe.com/en/topics/content-authenticity) - 行业见解和用例
- [理解 C2PA 清单](https://opensource.contentauthenticity.org/docs/manifest) - 技术深入探讨

---

## 🎯 用例和演示

### 行业应用

- **新闻和新闻业**：验证照片和视频的真实性（BBC、路透社试点）
- **相机制造商**：相机内 C2PA 签名（Leica、Nikon、Sony）
- **社交媒体**：平台上的内容来源（探索中）
- **AI 图像生成器**：标记 AI 生成的内容（Midjourney、DALL-E）
- **库存摄影**：证明原创作者身份（Adobe Stock、Shutterstock）

### 演示项目

- [C2PA 演示画廊](https://contentauthenticity.org/examples) - 带 C2PA 清单的示例图像
- [验证工具演示](https://contentcredentials.org/verify) - 尝试验证 C2PA 内容
- [交互式清单浏览器](https://opensource.contentauthenticity.org) - 探索清单结构

---

## 🏢 组织和生态系统

### 指导委员会成员

- Adobe
- Arm
- BBC
- Intel
- Microsoft
- Publicis Groupe
- Sony
- Truepic

### 采用者和合作伙伴

- **生成式 AI 提供商**：[OpenAI](https://openai.com/index/understanding-the-source-of-what-we-see-and-hear-online/)、[Google](https://blog.google/technology/ai/google-gen-ai-content-transparency-c2pa/)、[Meta](https://about.fb.com/news/2024/02/labeling-ai-generated-images-on-facebook-instagram-and-threads)
- **相机制造商**：Leica、Nikon、Sony、Canon
- **软件公司**：Adobe、Microsoft、Capture One
- **新闻组织**：BBC、纽约时报、路透社
- **社交平台**：探索集成中
- **认证机构**：DigiCert、GlobalSign 等

---

## 📰 新闻和更新

- [C2PA v2.2 规范发布](https://c2pa.org) - 最新版本（2025）
- [内容真实性倡议里程碑](https://contentauthenticity.org/news) - 行业采用更新
- [C2PA 在 X/Twitter 上](https://twitter.com/C2PA_Coalition) - 关注实时更新

---

## 🤝 社区

### 参与其中

- [Awesome C2PA GitHub Issues](https://github.com/paulortiz199928/awesome-c2pa/issues) - 提问和分享想法

### 为本项目做贡献

我们欢迎贡献！查看我们的[贡献指南](../../CONTRIBUTING.md)了解详情：
- 添加新资源
- 翻译规范
- 改进文档
- 报告问题

---

## 📋 贡献

欢迎贡献！请先阅读我们的[贡献指南](../../CONTRIBUTING.md)。

### 如何贡献

1. **添加资源**：提交 PR，包含新工具、库或文章
2. **翻译规范**：帮助将 C2PA 规范翻译成新语言
3. **修复错误**：报告或修复翻译错误、失效链接或过时信息
4. **改进内容**：增强描述、添加示例或重组章节

### 质量标准

我们接受以下资源：
- 积极维护（最近一年内更新）
- 文档完善
- 与 C2PA 实现或理解相关
- 开源（首选）或免费访问

---

## 🙏 致谢

- 感谢 [C2PA 组织](https://c2pa.org)开发开放标准
- 感谢[内容真实性倡议](https://contentauthenticity.org)推动采用
- 感谢所有帮助维护本资源的贡献者

---

**[⬆ 返回顶部](#目录)**

*最后更新：2025 年 11 月 | 由社区维护*
