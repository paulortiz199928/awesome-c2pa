---
title: 內容溯源與真實性標準
description: C2PA 內容來源與真實性標準綜合指南
template: splash
hero:
  title: C2PA 百科
  tagline: C2PA 內容來源與真實性標準綜合指南
  actions:
    - text: 快速入門
      link: /zh-tw/getting-started/quick-start/
      icon: right-arrow
      variant: primary
    - text: 檢視規範
      link: /specifications/
      icon: external
      variant: secondary
---

# Awesome C2PA [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> C2PA(內容來源與真實性聯盟)資源精選清單,包含多語言規範、工具、程式庫和學習資料。

**[English](../../README.md) | [简体中文](../zh-Hans/README.md) | 繁體中文 | [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Deutsch](../de/README.md) | [Français](../fr/README.md) | [Русский](../ru/README.md)**

C2PA 是一項開放技術標準,為發布者、創作者和消費者提供追溯不同類型媒體來源的能力。在 AI 生成內容的時代,C2PA 有助於驗證內容的真實性和來源。

## 🌟 亮點

**🌍 多語言官方規範** - 本專案提供首個由社群推動的 C2PA 官方規範多語言翻譯,讓全球開發者都能輕鬆理解 C2PA。

**🤝 協助改善翻譯** - 我們的翻譯採用 AI 輔助(DeepL),目前處於測試階段。歡迎母語人士[回報錯誤](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md)以協助提升品質!

## 目錄

- [官方規範(多語言)](#-官方規範多語言)
- [什麼是 C2PA?](#-什麼是-c2pa)
- [常見問題](#-常見問題)
- [官方資源](#-官方資源)
- [工具與程式庫](#-工具與程式庫)
  - [Rust](#rust)
  - [JavaScript/TypeScript](#javascripttypescript)
  - [Python](#python)
  - [Go](#go)
  - [Java](#java)
  - [其他語言](#其他語言)
- [命令列工具](#-命令列工具)
- [瀏覽器擴充功能與應用程式](#-應用程式)
- [學習資源](#-學習資源)
  - [教學課程](#教學課程)
  - [影片](#影片)
  - [文章與部落格](#文章與部落格)
- [使用案例與展示](#-使用案例與展示)
- [組織與生態系統](#-組織與生態系統)
- [新聞與更新](#-新聞與更新)
- [社群](#-社群)
- [貢獻](#-貢獻)

---

## 🌍 官方規範(多語言)

C2PA 規範 2.2 版提供多種語言版本。這些翻譯有助於全球開發者理解並在其應用程式中實作 C2PA。

| 語言 | 文件 | 狀態 | 方法 | 最後更新 |
|----------|----------|--------|--------|--------------|
| 🇬🇧 English | [C2PA Specification 2.2](../../docs/specifications/C2PA_Specification.pdf) | ✅ 官方版本 | C2PA Org | May 2025 |
| 🇨🇳 简体中文 | [C2PA 规范 2.2](../../docs/specifications/C2PA_Specification_zh-Hans.pdf) | 🔄 測試版 | AI + 審核 | 2025 |
| 🇹🇼 繁體中文 | [C2PA 規範 2.2](../../docs/specifications/C2PA_Specification_zh-Hans.pdf) | 🔄 測試版 | AI + 審核 | 2025 |
| 🇯🇵 日本語 | [C2PA 仕様 2.2](../../docs/specifications/C2PA_Specification_ja.pdf) | 🔄 測試版 | AI + 審核 | 2025 |
| 🇩🇪 Deutsch | [C2PA Spezifikation 2.2](../../docs/specifications/C2PA_Specification_de.pdf) | 🔄 測試版 | AI + 審核 | 2025 |
| 🇫🇷 Français | [Spécification C2PA 2.2](../../docs/specifications/C2PA_Specification_fr.pdf) | 🔄 測試版 | AI + 審核 | 2025 |
| 🇰🇷 한국어 | 即將推出 | 🚧 規劃中 | - | - |
| 🇪🇸 Español | 即將推出 | 🚧 規劃中 | - | - |
| 🇵🇹 Português | 即將推出 | 🚧 規劃中 | - | - |

> **翻譯聲明**:非英文翻譯採用 AI 輔助(DeepL)並經過社群審核。雖然我們力求準確,但仍可能存在錯誤。歡迎母語人士[回報問題](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md)或提交修正。英文版本仍為權威參考。

**快速導覽**:[檢視所有規範 →](../../docs/README.md)

---

## 🤔 什麼是 C2PA?

**C2PA(內容來源與真實性聯盟)**是一項開放標準,可在媒體檔案中加入經過加密簽署的中繼資料,以驗證內容來源和編輯歷史。

**主要優勢:**
- ✅ 驗證內容真實性並偵測竄改
- ✅ 追蹤從原始版本到目前版本的完整編輯歷史
- ✅ 識別 AI 生成或 AI 修改的內容
- ✅ 保護創作者署名和智慧財產權

**想深入瞭解?**
- 📖 [5 分鐘快速入門指南](quick-start.md) - 立即動手實作
- ❓ [完整常見問題](faq.md) - 解答 25+ 個詳細問題
- 📚 [技術規範](../../docs/README.md) - 深入探討標準

---

## ❓ 常見問題

最常見問題的快速解答:

<details>
<summary><b>什麼是 C2PA,它如何運作?</b></summary>

C2PA 在媒體檔案中加入經過加密簽署的中繼資料("manifest"),其中包含來源資訊。任何竄改都會破壞簽章,使修改行為可被偵測。它使用標準 PKI(如 HTTPS 憑證),而非區塊鏈。
</details>

<details>
<summary><b>C2PA 可以被移除嗎?它能偵測 AI 生成的圖片嗎?</b></summary>

**移除**:可以,這是設計使然。C2PA 在*存在時*證明真實性,而非防止移除。

**AI 偵測**:不會自動偵測。C2PA 記錄創作者聲明的內容。AI 工具必須自願在 manifest 中將其輸出標記為「AI 生成」。
</details>

<details>
<summary><b>哪些相機和軟體支援 C2PA?</b></summary>

**相機**:Leica(M11-P、SL3)、Sony(Alpha 1、A9 III、A7S III、A7 IV)、Nikon(Z6 III 計劃於 2025 年推出)可在拍攝時簽署照片。

**軟體**:Adobe Photoshop/Lightroom、Capture One 以及許多開源工具。

**費用**:標準和工具免費。憑證費用:每年約 50-500 美元。
</details>

**[→ 檢視所有 25+ 常見問題](faq.md)**,涵蓋技術細節、隱私、安全性和採用情況。

---

## 📚 官方資源

- [C2PA 官方網站](https://c2pa.org/) - 包含新聞和資訊的主要網站
- [C2PA 規範](https://c2pa.org/specifications/specifications/2.2/index.html) - 官方規範入口網站(v2.2)
- [C2PA GitHub 組織](https://github.com/c2pa-org) - 官方 GitHub 儲存庫
- [內容真實性倡議](https://contentauthenticity.org/) - Adobe 領導的支援 C2PA 的倡議

---

## 🛠️ 工具與程式庫

### Rust

- [c2pa-rs](https://github.com/contentauth/c2pa-rs) - 用於建立和驗證 C2PA manifest 的官方 Rust SDK。參考實作。

### JavaScript/TypeScript

- [c2pa-node-v2](https://github.com/contentauth/c2pa-node-v2) - C2PA Rust SDK 的官方 Node.js 繫結
- [c2pa-js](https://github.com/contentauth/c2pa-js) - 用於在瀏覽器中讀取 C2PA manifest 的 JavaScript 程式庫

### Python

- [c2pa-python](https://github.com/contentauth/c2pa-python) - C2PA Rust SDK 的官方 Python 繫結

### Java

- [c2pa-java](https://github.com/contentauth/c2pa-java) - C2PA SDK 的 Java 繫結

### 其他語言

- [c2pa-c](https://github.com/contentauth/c2pa-c) - C2PA 的 C 和 C++ 繫結
- [c2pa-ios](https://github.com/contentauth/c2pa-ios) - iOS 的 C2PA SDK
- 語言繫結持續擴展 - 請查看[官方 GitHub](https://github.com/contentauth/)以獲取更新

---

## 🔧 命令列工具

- [C2PA 命令列工具](https://github.com/contentauth/c2pa-rs/tree/main/cli) - 用於建立和檢查 C2PA manifest 的官方命令列工具
  - 建立、讀取和驗證 C2PA 內容
  - 跨平台:Windows、macOS、Linux
  - 支援圖片、影片、音訊

---

## 🌐 應用程式

- [Content Credentials Verify](https://contentcredentials.org/verify) - 用於驗證 C2PA 內容的官方網頁工具
---

## 📖 學習資源

### 教學課程

- [C2PA 快速入門指南](quick-start.md) - 5 分鐘 C2PA 實作入門
- [C2PA 開發者文件](https://opensource.contentauthenticity.org/docs) - 官方入門指南和文件
- [C2PA 開發者教學課程](https://opensource.contentauthenticity.org/docs/getting-started) - 逐步實作教學課程

### 影片

- [內容真實性倡議介紹](https://www.youtube.com/@contentauthenticity) - 包含教學影片的官方 YouTube 頻道
- [C2PA 技術概述](https://www.youtube.com/results?search_query=c2pa+technical) - 會議演講和技術簡報
- [Content Credentials 運作方式](https://contentauthenticity.org/how-it-works) - C2PA 實際運作的視覺化說明

### 文章與部落格

- [C2PA 官方網站](https://c2pa.org) - 新聞、更新和技術資源
- [Adobe 內容真實性部落格](https://blog.adobe.com/en/topics/content-authenticity) - 產業見解和使用案例
- [理解 C2PA Manifest](https://opensource.contentauthenticity.org/docs/manifest) - 技術深入探討

---

## 🎯 使用案例與展示

### 產業應用

- **新聞與新聞業**:驗證照片和影片真實性(BBC、Reuters 試用)
- **相機製造商**:機內 C2PA 簽署(Leica、Nikon、Sony)
- **社群媒體**:平台上的內容來源(探索中)
- **AI 圖像生成器**:標記 AI 生成的內容(Midjourney、DALL-E)
- **圖庫攝影**:證明原創作者身份(Adobe Stock、Shutterstock)


## 🏢 組織與生態系統

### 指導委員會成員

- Adobe
- Arm
- BBC
- Intel
- Microsoft
- Publicis Groupe
- Sony
- Truepic

### 採用者與合作夥伴

- **GenAI 提供者**:[OpenAI](https://openai.com/index/understanding-the-source-of-what-we-see-and-hear-online/)、[Google](https://blog.google/technology/ai/google-gen-ai-content-transparency-c2pa/)、[Meta](https://about.fb.com/news/2024/02/labeling-ai-generated-images-on-facebook-instagram-and-threads)
- **相機製造商**:Leica、Nikon、Sony、Canon
- **軟體公司**:Adobe、Microsoft、Capture One
- **新聞機構**:BBC、New York Times、Reuters
- **社群平台**:探索整合中
- **憑證授權機構**:DigiCert、GlobalSign 等

---

## 📰 新聞與更新

- [C2PA v2.2 規範發布](https://c2pa.org) - 最新版本(2025)
- [內容真實性倡議里程碑](https://contentauthenticity.org/news) - 產業採用更新
- [C2PA 在 X/Twitter](https://twitter.com/C2PA_Coalition) - 關注以獲取即時更新

---

## 🤝 社群

### 參與其中
- [Awesome C2PA GitHub Issues](https://github.com/paulortiz199928/awesome-c2pa/issues) - 提問和分享想法

### 為本專案做出貢獻

我們歡迎貢獻!詳情請參閱我們的[貢獻指南](../../CONTRIBUTING.md):
- 新增資源
- 翻譯規範
- 改進文件
- 回報問題

---

## 📋 貢獻

歡迎貢獻!請先閱讀我們的[貢獻準則](../../CONTRIBUTING.md)。

### 如何貢獻

1. **新增資源**:提交包含新工具、程式庫或文章的 PR
2. **翻譯規範**:協助將 C2PA 規範翻譯成新語言
3. **修正錯誤**:回報或修正翻譯錯誤、失效連結或過時資訊
4. **改進內容**:增強描述、新增範例或重新組織章節

### 品質標準

我們接受以下資源:
- 積極維護(過去一年內有更新)
- 文件完善
- 與 C2PA 實作或理解相關
- 開源(優先)或可自由存取

---

## 🙏 致謝

- 感謝 [C2PA 組織](https://c2pa.org)開發開放標準
- 感謝[內容真實性倡議](https://contentauthenticity.org)推廣採用
- 感謝所有協助維護本資源的貢獻者

---

**[⬆ 回到頂部](#目錄)**

*最後更新:2025 年 11 月 | 由社群維護*
