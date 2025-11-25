# Awesome C2PA [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> C2PA（Coalition for Content Provenance and Authenticity）に関する厳選されたリソースのリスト。多言語仕様、ツール、ライブラリ、学習教材を含みます。

**[English](../../README.md) | [简体中文](../zh-Hans/README.md) | [繁體中文](../zh-Hant/README.md) | 日本語 | [한국어](../ko/README.md) | [Deutsch](../de/README.md) | [Français](../fr/README.md) | [Русский](../ru/README.md)**

C2PAは、パブリッシャー、クリエイター、コンシューマーがさまざまな種類のメディアの起源を追跡できるようにするオープン技術標準です。AI生成コンテンツの時代において、C2PAはコンテンツの真正性と来歴の検証に役立ちます。

## 🌟 ハイライト

**🌍 多言語公式仕様** - このプロジェクトは、C2PA公式仕様のコミュニティ主導による初の多言語翻訳を提供し、世界中の開発者がC2PAにアクセスできるようにします。

**🤝 翻訳の改善にご協力を** - 翻訳はAI支援（DeepL）によるベータ版です。ネイティブスピーカーの方は、[エラーを報告](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md)して品質向上にご協力ください！

## 目次

- [公式仕様（多言語）](#-公式仕様多言語)
- [C2PAとは？](#-c2paとは)
- [よくある質問](#-よくある質問)
- [公式リソース](#-公式リソース)
- [ツールとライブラリ](#-ツールとライブラリ)
  - [Rust](#rust)
  - [JavaScript/TypeScript](#javascripttypescript)
  - [Python](#python)
  - [Go](#go)
  - [Java](#java)
  - [その他の言語](#その他の言語)
- [コマンドラインツール](#-コマンドラインツール)
- [ブラウザ拡張機能とアプリケーション](#-アプリケーション)
- [学習リソース](#-学習リソース)
  - [チュートリアル](#チュートリアル)
  - [動画](#動画)
  - [記事とブログ](#記事とブログ)
- [ユースケースとデモ](#-ユースケースとデモ)
- [組織とエコシステム](#-組織とエコシステム)
- [ニュースと最新情報](#-ニュースと最新情報)
- [コミュニティ](#-コミュニティ)
- [貢献](#-貢献)

---

## 🌍 公式仕様（多言語）

C2PA仕様バージョン2.2は複数の言語で利用できます。これらの翻訳は、世界中の開発者がアプリケーションにC2PAを理解し実装するのに役立ちます。

| 言語 | ドキュメント | ステータス | 方法 | 最終更新 |
|----------|----------|--------|--------|--------------|
| 🇬🇧 English | [C2PA Specification 2.2](../../docs/specifications/C2PA_Specification.pdf) | ✅ 公式 | C2PA Org | 2025年5月 |
| 🇨🇳 简体中文 | [C2PA 规范 2.2](../../docs/specifications/C2PA_Specification_zh-Hans.pdf) | 🔄 ベータ | AI + レビュー | 2025年 |
| 🇯🇵 日本語 | [C2PA 仕様 2.2](../../docs/specifications/C2PA_Specification_ja.pdf) | 🔄 ベータ | AI + レビュー | 2025年 |
| 🇩🇪 Deutsch | [C2PA Spezifikation 2.2](../../docs/specifications/C2PA_Specification_de.pdf) | 🔄 ベータ | AI + レビュー | 2025年 |
| 🇫🇷 Français | [Spécification C2PA 2.2](../../docs/specifications/C2PA_Specification_fr.pdf) | 🔄 ベータ | AI + レビュー | 2025年 |
| 🇰🇷 한국어 | Coming soon | 🚧 計画中 | - | - |
| 🇪🇸 Español | Coming soon | 🚧 計画中 | - | - |
| 🇵🇹 Português | Coming soon | 🚧 計画中 | - | - |

> **翻訳に関する注意**: 英語以外の翻訳はAI支援（DeepL）とコミュニティレビューによるものです。正確性を目指していますが、エラーが存在する可能性があります。ネイティブスピーカーの方は、[問題を報告](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md)するか、修正を提出してください。英語版が権威のある参照元です。

**クイックナビゲーション**: [すべての仕様を表示 →](../../docs/README.md)

---

## 🤔 C2PAとは？

**C2PA（Coalition for Content Provenance and Authenticity）**は、メディアファイルに暗号署名付きメタデータを追加し、コンテンツの起源と編集履歴の検証を可能にするオープン標準です。

**主な利点:**
- ✅ コンテンツの真正性を検証し、改ざんを検出
- ✅ オリジナルから現在のバージョンまでの完全な編集履歴を追跡
- ✅ AI生成またはAI修正されたコンテンツを識別
- ✅ クリエイターの帰属と知的財産を保護

**さらに詳しく知りたい方は:**
- 📖 [5分間クイックスタートガイド](quick-start.md) - すぐに実践
- ❓ [完全版FAQ](faq.md) - 25以上の詳細な質問に回答
- 📚 [技術仕様](../../docs/README.md) - 標準の詳細

---

## ❓ よくある質問

最も一般的な質問への簡単な回答:

<details>
<summary><b>C2PAとは何ですか？どのように機能しますか？</b></summary>

C2PAは、来歴情報を含む暗号署名付きメタデータ（「manifest（マニフェスト）」）をメディアファイルに追加します。改ざんがあると署名が破損するため、変更が検出可能になります。C2PAは、ブロックチェーンではなく標準のPKI（HTTPSの証明書と同様）を使用します。
</details>

<details>
<summary><b>C2PAは削除できますか？AI生成画像を検出できますか？</b></summary>

**削除について**: はい、設計上削除可能です。C2PAは、削除を防ぐのではなく、存在する場合に真正性を証明します。

**AI検出について**: 自動的には検出しません。C2PAはクリエイターが宣言した内容を記録します。AIツールは、マニフェストに「AI生成」として自主的にラベル付けする必要があります。
</details>

<details>
<summary><b>どのカメラとソフトウェアがC2PAをサポートしていますか？</b></summary>

**カメラ**: Leica（M11-P、SL3）、Sony（Alpha 1、A9 III、A7S III、A7 IV）、Nikon（Z6 IIIは2025年に計画）が撮影時に写真に署名できます。

**ソフトウェア**: Adobe Photoshop/Lightroom、Capture One、および多くのオープンソースツール。

**コスト**: 標準とツールは無料です。証明書の費用: 年間約$50-500。
</details>

**[→ 25以上のFAQをすべて表示](faq.md)** 技術的な詳細、プライバシー、セキュリティ、採用について。

---

## 📚 公式リソース

- [C2PA公式ウェブサイト](https://c2pa.org/) - ニュースと情報を含むメインサイト
- [C2PA仕様](https://c2pa.org/specifications/specifications/2.2/index.html) - 公式仕様ポータル（v2.2）
- [C2PA GitHub Organization](https://github.com/c2pa-org) - 公式GitHubリポジトリ
- [Content Authenticity Initiative](https://contentauthenticity.org/) - C2PAをサポートするAdobe主導のイニシアチブ

---

## 🛠️ ツールとライブラリ

### Rust

- [c2pa-rs](https://github.com/contentauth/c2pa-rs) - C2PAマニフェストの作成と検証のための公式Rust SDK。参照実装。

### JavaScript/TypeScript

- [c2pa-node-v2](https://github.com/contentauth/c2pa-node-v2) - C2PA Rust SDKの公式Node.jsバインディング
- [c2pa-js](https://github.com/contentauth/c2pa-js) - ブラウザでC2PAマニフェストを読み取るためのJavaScriptライブラリ

### Python

- [c2pa-python](https://github.com/contentauth/c2pa-python) - C2PA Rust SDKの公式Pythonバインディング

### Java

- [c2pa-java](https://github.com/contentauth/c2pa-java) - C2PA SDKのJavaバインディング

### その他の言語

- [c2pa-c](https://github.com/contentauth/c2pa-c) - C2PAのCおよびC++バインディング
- [c2pa-ios](https://github.com/contentauth/c2pa-ios) - iOS用C2PA SDK
- 言語バインディングは拡張中 - 更新については[公式GitHub](https://github.com/contentauth/)を確認してください

---

## 🔧 コマンドラインツール

- [C2PAコマンドラインツール](https://github.com/contentauth/c2pa-rs/tree/main/cli) - C2PAマニフェストの作成と検査のための公式コマンドラインツール
  - C2PAコンテンツの作成、読み取り、検証
  - クロスプラットフォーム: Windows、macOS、Linux
  - 画像、動画、音声をサポート

---

## 🌐 アプリケーション

- [Content Credentials Verify](https://contentcredentials.org/verify) - C2PAコンテンツを検証するための公式Webツール
---

## 📖 学習リソース

### チュートリアル

- [C2PAクイックスタートガイド](quick-start.md) - C2PA実装への5分間の入門
- [C2PA開発者ドキュメント](https://opensource.contentauthenticity.org/docs) - 公式入門ガイドとドキュメント
- [C2PA開発者チュートリアル](https://opensource.contentauthenticity.org/docs/getting-started) - ステップバイステップの実装チュートリアル

### 動画

- [Content Authenticity Initiative入門](https://www.youtube.com/@contentauthenticity) - 教育ビデオを含む公式YouTubeチャンネル
- [C2PA技術概要](https://www.youtube.com/results?search_query=c2pa+technical) - カンファレンストークと技術プレゼンテーション
- [Content Credentialsの仕組み](https://contentauthenticity.org/how-it-works) - C2PAの動作を視覚的に説明

### 記事とブログ

- [C2PA公式ウェブサイト](https://c2pa.org) - ニュース、更新情報、技術リソース
- [Adobe Content Authenticityブログ](https://blog.adobe.com/en/topics/content-authenticity) - 業界の洞察とユースケース
- [C2PAマニフェストの理解](https://opensource.contentauthenticity.org/docs/manifest) - 技術的な詳細

---

## 🎯 ユースケースとデモ

### 業界アプリケーション

- **ニュースとジャーナリズム**: 写真と動画の真正性を検証（BBC、Reutersのトライアル）
- **カメラメーカー**: カメラ内C2PA署名（Leica、Nikon、Sony）
- **ソーシャルメディア**: プラットフォーム上のコンテンツ来歴（検討中）
- **AI画像生成**: AI生成コンテンツのラベル付け（Midjourney、DALL-E）
- **ストックフォトグラフィー**: オリジナルの著作権の証明（Adobe Stock、Shutterstock）


## 🏢 組織とエコシステム

### 運営委員会メンバー

- Adobe
- Arm
- BBC
- Intel
- Microsoft
- Publicis Groupe
- Sony
- Truepic

### 採用者とパートナー

- **GenAIプロバイダー**: [OpenAI](https://openai.com/index/understanding-the-source-of-what-we-see-and-hear-online/)、[Google](https://blog.google/technology/ai/google-gen-ai-content-transparency-c2pa/)、[Meta](https://about.fb.com/news/2024/02/labeling-ai-generated-images-on-facebook-instagram-and-threads)
- **カメラメーカー**: Leica、Nikon、Sony、Canon
- **ソフトウェア企業**: Adobe、Microsoft、Capture One
- **報道機関**: BBC、New York Times、Reuters
- **ソーシャルプラットフォーム**: 統合を検討中
- **認証機関**: DigiCert、GlobalSignなど

---

## 📰 ニュースと最新情報

- [C2PA v2.2仕様リリース](https://c2pa.org) - 最新バージョン（2025年）
- [Content Authenticity Initiativeマイルストーン](https://contentauthenticity.org/news) - 業界採用の更新情報
- [C2PA on X/Twitter](https://twitter.com/C2PA_Coalition) - リアルタイムの更新情報をフォロー

---

## 🤝 コミュニティ

### 参加する
- [Awesome C2PA GitHub Issues](https://github.com/paulortiz199928/awesome-c2pa/issues) - 質問をしたり、アイデアを共有したりできます

### このプロジェクトへの貢献

貢献を歓迎します！詳細については[貢献ガイド](../../CONTRIBUTING.md)をご覧ください:
- 新しいリソースの追加
- 仕様の翻訳
- ドキュメントの改善
- 問題の報告

---

## 📋 貢献

貢献を歓迎します！まず[貢献ガイドライン](../../CONTRIBUTING.md)をお読みください。

### 貢献方法

1. **リソースの追加**: 新しいツール、ライブラリ、記事を含むPRを提出
2. **仕様の翻訳**: C2PA仕様の新しい言語への翻訳を支援
3. **エラーの修正**: 翻訳エラー、リンク切れ、古い情報を報告または修正
4. **コンテンツの改善**: 説明の強化、例の追加、セクションの再構成

### 品質基準

次の基準を満たすリソースを受け入れます:
- 積極的にメンテナンスされている（過去1年以内に更新）
- よくドキュメント化されている
- C2PAの実装または理解に関連している
- オープンソース（推奨）または自由にアクセス可能

---

## 🙏 謝辞

- オープン標準を開発した[C2PA Organization](https://c2pa.org)に感謝します
- 採用を促進している[Content Authenticity Initiative](https://contentauthenticity.org)に感謝します
- このリソースの維持を支援しているすべての貢献者に感謝します

---

**[⬆ トップに戻る](#目次)**

*最終更新: 2025年11月 | コミュニティによってメンテナンス*
