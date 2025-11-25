# C2PAクイックスタートガイド

5分でC2PAを始めましょう！このガイドは、C2PA署名付きコンテンツを理解、検証、作成する方法を説明します。

## 📋 目次

1. [C2PAの理解](#c2paの理解)
2. [C2PAコンテンツの検証](#c2paコンテンツの検証)
3. [C2PAコンテンツの作成](#c2paコンテンツの作成)
4. [次のステップ](#次のステップ)

---

## C2PAの理解

### 知っておくべきこと

**C2PA**は、次の情報を含む暗号署名付きの「manifest（マニフェスト）」をメディアファイルに追加します:
- **誰が**: クリエイター/編集者のID
- **何を**: 実行されたアクション（作成、編集、AI生成）
- **いつ**: タイムスタンプ
- **どのように**: 使用されたツールと設定
- **どこから**: ソース素材（材料）

### 30秒で理解する主要概念

```
オリジナル写真 → [C2PAマニフェストを追加] → 署名付き写真
                     ↓
              次を含むメタデータ:
              • クリエイター: John Doe
              • カメラ: Nikon Z9
              • 日付: 2025-11-21
              • GPS: 37.7749°N, 122.4194°W
              • 署名: ✓ 有効
```

編集する場合:
```
署名付き写真 → [Photoshopで編集] → 新しい署名付き写真
                                          ↓
                                   新しいマニフェストが
                                   オリジナルを「材料」として参照
```

**結果**: オリジナルから現在のバージョンまでの完全な来歴チェーン。

---

## C2PAコンテンツの検証

### 方法1: オンラインツール（最も簡単）

**インストール不要！**

1. https://contentcredentials.org/verify にアクセス
2. 任意の画像/動画/文書をドラッグ＆ドロップ
3. 来歴情報を表示:
   - クリエイターID
   - 編集履歴
   - 署名ステータス
   - オリジナルコンテンツ（利用可能な場合）

**今すぐ試す**: https://contentauthenticity.org/examples のサンプル画像で

### 方法2: ブラウザ拡張機能

**ブラウジング中の自動検証:**

1. [Content Credentials拡張機能](https://chrome.google.com/webstore)をインストール
   - Chrome、Edge、Braveで利用可能
2. 通常通りブラウジング
3. 拡張機能が自動的にC2PAコンテンツを検出
4. アイコンをクリックして来歴の詳細を表示

### 方法3: コマンドライン

**開発者とパワーユーザー向け:**

#### c2patoolのインストール

```bash
# macOS/Linux（Cargoを使用）
cargo install c2patool

# macOS（Homebrewを使用）
brew install c2patool

# Windows
# 次からダウンロード: https://github.com/contentauth/c2patool/releases
```

#### ファイルの検証

```bash
# 基本的な検証
c2patool photo.jpg

# 詳細なJSON出力
c2patool photo.jpg --detailed

# マニフェストをJSONファイルに保存
c2patool photo.jpg --output manifest.json

# 複数のファイルをチェック
c2patool *.jpg
```

#### 出力例

```
File: photo.jpg
Status: ✓ Valid C2PA signature

Creator: John Doe (john@example.com)
Created: 2025-11-21T10:30:00Z
Camera: Nikon Z9
Signature: Valid
Certificate: DigiCert
Actions: Captured
```

### 方法4: プログラムから

**アプリに検証を統合:**

#### JavaScript/Node.js

```javascript
const c2pa = require('c2pa-node');

async function verify(imagePath) {
  const manifest = await c2pa.read(imagePath);

  if (manifest) {
    console.log('Creator:', manifest.claim.creator);
    console.log('Created:', manifest.claim.created);
    console.log('Valid:', manifest.validation_status);
  } else {
    console.log('No C2PA data found');
  }
}

verify('photo.jpg');
```

#### Python

```python
from c2pa import Reader

reader = Reader('photo.jpg')
manifest = reader.manifest()

if manifest:
    print(f"Creator: {manifest.creator}")
    print(f"Created: {manifest.created}")
    print(f"Valid: {manifest.is_valid}")
else:
    print("No C2PA data found")
```

---

## C2PAコンテンツの作成

### 方法1: サポートされているソフトウェアを使用

**コーディング不要:**

#### Adobe Photoshop/Lightroom

1. Photoshop/Lightroomで画像を開く
2. **編集 → Content Credentials**に移動
3. クリエイター情報を入力
4. ファイルを保存 → C2PAマニフェストが自動的に追加される

#### C2PA組み込みカメラ

- **Nikon Z9/Z8**: カメラ設定で有効化 → 撮影時に写真に署名
- **Leica M11-P/SL3**: 自動署名が有効
- **Sonyアルファシリーズ**: ファームウェア更新で有効化

### 方法2: コマンドライン（c2patool）

#### 前提条件

署名証明書が必要です:

**テスト用（自己署名）:**
```bash
# テスト証明書を生成（バリデーターによって信頼されない）
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes
```

**本番用:**
- 信頼されたCA（DigiCert、GlobalSignなど）から証明書を購入
- C2PAキー使用要件を指定

#### マニフェストの作成

`manifest.json`を作成:

```json
{
  "claim_generator": "my-app/1.0",
  "assertions": [
    {
      "label": "stds.schema-org.CreativeWork",
      "data": {
        "@context": "https://schema.org",
        "@type": "CreativeWork",
        "author": [
          {
            "@type": "Person",
            "name": "John Doe"
          }
        ]
      }
    },
    {
      "label": "c2pa.actions",
      "data": {
        "actions": [
          {
            "action": "c2pa.created"
          }
        ]
      }
    }
  ]
}
```

#### ファイルに署名

```bash
# 証明書で署名
c2patool photo.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed_photo.jpg

# 動作を確認
c2patool signed_photo.jpg
```

### 方法3: プログラムから

#### Rust

```rust
use c2pa::{Builder, SigningAlg};

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let mut builder = Builder::from_file("input.jpg")?;

    // クリエイターアサーションを追加
    builder.add_assertion("stds.schema-org.CreativeWork",
        r#"{"author": [{"name": "John Doe"}]}"#)?;

    // 署名して保存
    let signer = get_signer(); // 証明書/鍵
    builder.sign("output.jpg", signer)?;

    Ok(())
}
```

#### JavaScript/Node.js

```javascript
const c2pa = require('c2pa-node');

async function sign(inputPath, outputPath) {
  const manifest = {
    claim_generator: 'my-app/1.0',
    assertions: [
      {
        label: 'stds.schema-org.CreativeWork',
        data: {
          author: [{ name: 'John Doe' }]
        }
      }
    ]
  };

  const signer = {
    cert: 'path/to/cert.pem',
    key: 'path/to/key.pem'
  };

  await c2pa.sign(inputPath, outputPath, manifest, signer);
  console.log('Signed successfully!');
}

sign('input.jpg', 'output.jpg');
```

#### Python

```python
from c2pa import Builder, Signer

# ビルダーを作成
builder = Builder.from_file('input.jpg')

# アサーションを追加
builder.add_assertion('stds.schema-org.CreativeWork', {
    'author': [{'name': 'John Doe'}]
})

# 署名
signer = Signer('cert.pem', 'key.pem')
builder.sign('output.jpg', signer)

print('Signed successfully!')
```

### 方法4: 署名付きコンテンツの編集（来歴の保存）

C2PA署名付きコンテンツを編集する場合、オリジナルを「材料」として参照します:

```bash
# 編集してチェーンを保存
c2patool edited_photo.jpg \
  --parent original_photo.jpg \
  --manifest edit_manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output final_photo.jpg
```

新しいマニフェストは`original_photo.jpg`を材料として参照し、完全な履歴を保存します。

---

## 次のステップ

### さらに学ぶ

**仕様を理解する:**
- [English](../../docs/specifications/C2PA_Specification.pdf)
- [中文](../../docs/specifications/C2PA_Specification_zh-Hans.pdf)
- [日本語](../../docs/specifications/C2PA_Specification_ja.pdf)
- [Deutsch](../../docs/specifications/C2PA_Specification_de.pdf)

**ツールを探索:**
- [ツールとライブラリ](README.md#ツールとライブラリ) - すべての主要言語向けSDK
- [公式ドキュメント](https://opensource.contentauthenticity.org/docs)

**よくある質問:**
- [FAQ](faq.md) - 25以上のよくある質問
- [GitHub Discussions](https://github.com/c2pa-org/../../docs/specifications/discussions)

### チュートリアルと例

**公式チュートリアル:**
- [C2PA開発者チュートリアル](https://opensource.contentauthenticity.org/docs/tutorial)
- [マニフェストの作成](https://opensource.contentauthenticity.org/docs/manifest/guide)
- [アサーションリファレンス](https://opensource.contentauthenticity.org/docs/manifest/assertions)

**コード例:**
- [c2pa-rs Examples](https://github.com/contentauth/c2pa-rs/tree/main/sdk/examples)
- [c2pa-node Examples](https://github.com/contentauth/c2pa-node/tree/main/examples)
- [c2pa-python Examples](https://github.com/contentauth/c2pa-python/tree/main/examples)

### 本番デプロイ

**公開前に:**

1. **本番証明書を取得**
   - 信頼されたCA（DigiCert、GlobalSignなど）から購入
   - C2PA互換のキー使用を確認
   - コスト: 年間約$50-500

2. **セキュアなキー保管**
   - 秘密鍵にはハードウェアセキュリティモジュール（HSM）を使用
   - またはクラウドHSM（AWS CloudHSM、Azure Key Vault）
   - ソース管理に鍵をコミットしない

3. **徹底的なテスト**
   - 複数のバリデーターで署名を検証
   - 異なるファイル形式でテスト
   - クロスプラットフォーム互換性を確認

4. **監視とメンテナンス**
   - 証明書のローテーションを実装
   - 失効を監視
   - SDKを最新に保つ

### アプリケーションとの統合

**主要な統合ポイント:**

```
アプリのワークフロー:

1. コンテンツの作成/アップロード
   ↓
2. [C2PAマニフェストを追加] ← 統合ポイント
   ↓
3. 証明書で署名
   ↓
4. 署名付きコンテンツを保存/公開
   ↓
5. [オプション] 表示時に検証 ← 別の統合ポイント
```

**一般的な統合時間:**
- シンプルな検証: 1-2日
- 基本的な署名: 3-5日
- 完全な本番デプロイ: 2-4週間

### 証明書の取得

**テスト（無料）:**
- 自己署名証明書
- 開発のみに適している
- バリデーターによって信頼されない

**本番:**
- **DigiCert**: https://www.digicert.com/
- **GlobalSign**: https://www.globalsign.com/
- **Entrust**: https://www.entrust.com/
- C2PAキー使用拡張付きの証明書をリクエスト

### コミュニティに参加

**ヘルプを得る:**
- [GitHub Issues](https://github.com/c2pa-org/../../docs/specifications/issues) - バグ報告
- [GitHub Discussions](https://github.com/c2pa-org/../../docs/specifications/discussions) - 質問
- [C2PAウェブサイト](https://c2pa.org) - 公式リソース

**貢献:**
- [awesome-c2pa](README.md) - リソースの追加、ドキュメントの翻訳
- [C2PA Implementations](https://github.com/contentauth) - コードの貢献
- [Content Authenticity Initiative](https://contentauthenticity.org) - ムーブメントに参加

---

## クイックリファレンスカード

### コンテンツの検証
```bash
c2patool image.jpg
```

### コンテンツへの署名
```bash
c2patool input.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed.jpg
```

### Webから確認
```
https://contentcredentials.org/verify
```

### 一般的なマニフェストテンプレート
```json
{
  "claim_generator": "app-name/version",
  "assertions": [
    {
      "label": "stds.schema-org.CreativeWork",
      "data": {
        "author": [{"name": "クリエイター名"}]
      }
    }
  ]
}
```

---

## トラブルシューティング

### "No C2PA data found"
- ファイルにC2PAマニフェストがない可能性
- メタデータが削除された可能性
- 別のファイル形式を試す

### "Invalid signature"
- 署名後にファイルが変更された
- 証明書が失効または期限切れ
- トラストチェーンが破損

### "Certificate not trusted"
- 自己署名証明書を使用（テストでは予想される）
- CAがトラストリストにない
- 必要に応じてカスタムトラストアンカーを追加

### パフォーマンスの問題
- C2PAはマニフェストあたり約10-50KBを追加（最小限）
- 署名は一般的なファイルで1秒未満
- 検証はほぼ瞬時

---

**始める準備はできましたか？** 上記の方法を選択して、始めましょう！

**質問はありますか？** [FAQ](faq.md)を確認するか、[イシューを開いて](https://github.com/paulortiz199928/awesome-c2pa/issues)ください。

---

*最終更新: 2025年11月*
