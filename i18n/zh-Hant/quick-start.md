# C2PA 快速入門指南

5 分鐘開始使用 C2PA!本指南將協助您理解、驗證和建立 C2PA 簽署的內容。

## 📋 目錄

1. [理解 C2PA](#理解-c2pa)
2. [驗證 C2PA 內容](#驗證-c2pa-內容)
3. [建立 C2PA 內容](#建立-c2pa-內容)
4. [下一步](#下一步)

---

## 理解 C2PA

### 您需要知道的

**C2PA** 在您的媒體檔案中新增經過加密簽署的「manifest」,包含:
- **誰**:創作者/編輯者身份
- **什麼**:執行的動作(建立、編輯、AI 生成)
- **何時**:時間戳記
- **如何**:使用的工具和設定
- **從**:來源素材(ingredients)

### 30 秒內掌握關鍵概念

```
原始照片 → [新增 C2PA Manifest] → 已簽署照片
                     ↓
              包含中繼資料:
              • 創作者:John Doe
              • 相機:Nikon Z9
              • 日期:2025-11-21
              • GPS:37.7749°N, 122.4194°W
              • 簽章:✓ 有效
```

當您編輯時:
```
已簽署照片 → [在 Photoshop 中編輯] → 新的已簽署照片
                                          ↓
                                   新 manifest 引用
                                   原始照片為「ingredient」
```

**結果**:從原始版本到目前版本的完整來源鏈。

---

## 驗證 C2PA 內容

### 方法 1:線上工具(最簡單)

**無需安裝!**

1. **訪問驗證工具**:打開網頁瀏覽器並訪問 https://contentcredentials.org/verify 以使用官方 C2PA 驗證工具。

2. **上傳媒體檔案**:將圖片、影片或文件拖放到驗證頁面,或點擊瀏覽並從裝置中選擇檔案。

3. **檢視來源資訊**:檢查顯示的資訊,包括:
   - 創作者身份
   - 建立日期
   - 編輯歷史
   - 使用的工具和軟體

4. **驗證簽章狀態**:確認簽章顯示為「有效」並帶有綠色勾號,這表明內容自簽章後未被竄改。

**立即嘗試**範例圖片:https://contentauthenticity.org/examples

### 方法 2:瀏覽器擴充功能

**瀏覽時自動驗證:**

1. 安裝 [Content Credentials Extension](https://chrome.google.com/webstore)
   - 適用於 Chrome、Edge、Brave
2. 正常瀏覽
3. 擴充功能自動偵測 C2PA 內容
4. 點選圖示以檢視來源詳情

### 方法 3:命令列

**適用於開發者和進階使用者:**

#### 安裝 c2patool

```bash
# macOS/Linux(使用 Cargo)
cargo install c2patool

# macOS(使用 Homebrew)
brew install c2patool

# Windows
# 從以下位置下載:https://github.com/contentauth/c2patool/releases
```

#### 驗證檔案

```bash
# 基本驗證
c2patool photo.jpg

# 詳細 JSON 輸出
c2patool photo.jpg --detailed

# 將 manifest 儲存到 JSON 檔案
c2patool photo.jpg --output manifest.json

# 檢查多個檔案
c2patool *.jpg
```

#### 範例輸出

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

### 方法 4:以程式方式

**將驗證整合到您的應用程式:**

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

## 建立 C2PA 內容

### 方法 1:使用支援的軟體

**無需編碼:**

#### Adobe Photoshop/Lightroom

1. 在 Photoshop/Lightroom 中開啟圖片
2. 前往**編輯 → Content Credentials**
3. 填寫創作者資訊
4. 儲存檔案 → 自動新增 C2PA manifest

#### 內建 C2PA 的相機

- **Nikon Z9/Z8**:在相機設定中啟用 → 拍攝時簽署照片
- **Leica M11-P/SL3**:已啟用自動簽署
- **Sony Alpha 系列**:透過韌體更新啟用

### 方法 2:命令列(c2patool)

#### 先決條件

您需要一個簽署憑證:

**用於測試(自簽):**
```bash
# 產生測試憑證(驗證者不信任)
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes
```

**用於生產:**
- 從受信任的 CA 購買憑證(DigiCert、GlobalSign 等)
- 指定 C2PA 金鑰使用要求

#### 建立 Manifest

建立 `manifest.json`:

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

#### 簽署檔案

```bash
# 使用您的憑證簽署
c2patool photo.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed_photo.jpg

# 驗證它是否有效
c2patool signed_photo.jpg
```

### 方法 3:以程式方式

#### Rust

```rust
use c2pa::{Builder, SigningAlg};

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let mut builder = Builder::from_file("input.jpg")?;

    // 新增創作者 assertion
    builder.add_assertion("stds.schema-org.CreativeWork",
        r#"{"author": [{"name": "John Doe"}]}"#)?;

    // 簽署並儲存
    let signer = get_signer(); // 您的憑證/金鑰
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

# 建立 builder
builder = Builder.from_file('input.jpg')

# 新增 assertions
builder.add_assertion('stds.schema-org.CreativeWork', {
    'author': [{'name': 'John Doe'}]
})

# 簽署
signer = Signer('cert.pem', 'key.pem')
builder.sign('output.jpg', signer)

print('Signed successfully!')
```

### 方法 4:編輯已簽署的內容(保留來源)

編輯 C2PA 簽署的內容時,將原始內容引用為「ingredient」:

```bash
# 編輯並保留鏈
c2patool edited_photo.jpg \
  --parent original_photo.jpg \
  --manifest edit_manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output final_photo.jpg
```

新 manifest 將引用 `original_photo.jpg` 作為 ingredient,保留完整歷史。

---

## 下一步

### 進一步學習

**理解規範:**
- [English](../../docs/specifications/C2PA_Specification.pdf)
- [简体中文](../../docs/specifications/C2PA_Specification_zh-Hans.pdf)
- [繁體中文](../../docs/specifications/C2PA_Specification_zh-Hans.pdf)
- [日本語](../../docs/specifications/C2PA_Specification_ja.pdf)
- [Deutsch](../../docs/specifications/C2PA_Specification_de.pdf)

**探索工具:**
- [工具與程式庫](README.md#工具與程式庫) - 所有主要語言的 SDK
- [官方文件](https://opensource.contentauthenticity.org/docs)

**常見問題:**
- [FAQ](faq.md) - 25+ 常見問題
- [GitHub Discussions](https://github.com/c2pa-org/../../docs/specifications/discussions)

### 教學課程與範例

**官方教學課程:**
- [C2PA 開發者教學課程](https://opensource.contentauthenticity.org/docs/tutorial)
- [建立 Manifest](https://opensource.contentauthenticity.org/docs/manifest/guide)
- [Assertion 參考](https://opensource.contentauthenticity.org/docs/manifest/assertions)

**程式碼範例:**
- [c2pa-rs 範例](https://github.com/contentauth/c2pa-rs/tree/main/sdk/examples)
- [c2pa-node 範例](https://github.com/contentauth/c2pa-node/tree/main/examples)
- [c2pa-python 範例](https://github.com/contentauth/c2pa-python/tree/main/examples)

### 生產部署

**上線前:**

1. **取得生產憑證**
   - 從受信任的 CA 購買(DigiCert、GlobalSign 等)
   - 確保 C2PA 相容的金鑰使用
   - 費用:每年約 50-500 美元

2. **安全金鑰儲存**
   - 對私密金鑰使用硬體安全模組(HSM)
   - 或雲端 HSM(AWS CloudHSM、Azure Key Vault)
   - 切勿將金鑰提交到原始碼控制

3. **徹底測試**
   - 使用多個驗證器驗證簽章
   - 測試不同的檔案格式
   - 檢查跨平台相容性

4. **監控與維護**
   - 實作憑證輪換
   - 監控撤銷
   - 保持 SDK 更新

### 與您的應用程式整合

**關鍵整合點:**

```
您的應用程式工作流程:

1. 內容建立/上傳
   ↓
2. [新增 C2PA Manifest] ← 您的整合點
   ↓
3. 使用憑證簽署
   ↓
4. 儲存/發布已簽署的內容
   ↓
5. [選用]在顯示時驗證 ← 另一個整合點
```

**典型整合時間:**
- 簡單驗證:1-2 天
- 基本簽署:3-5 天
- 完整生產部署:2-4 週

### 取得憑證

**測試(免費):**
- 自簽憑證
- 僅適用於開發
- 驗證者不信任

**生產:**
- **DigiCert**:https://www.digicert.com/
- **GlobalSign**:https://www.globalsign.com/
- **Entrust**:https://www.entrust.com/
- 請求具有 C2PA 金鑰使用擴充功能的憑證

### 加入社群

**取得協助:**
- [GitHub Issues](https://github.com/c2pa-org/../../docs/specifications/issues) - 錯誤回報
- [GitHub Discussions](https://github.com/c2pa-org/../../docs/specifications/discussions) - 問題
- [C2PA 網站](https://c2pa.org) - 官方資源

**貢獻:**
- [awesome-c2pa](README.md) - 新增資源、翻譯文件
- [C2PA 實作](https://github.com/contentauth) - 貢獻程式碼
- [內容真實性倡議](https://contentauthenticity.org) - 加入運動

---

## 快速參考卡

### 驗證內容
```bash
c2patool image.jpg
```

### 簽署內容
```bash
c2patool input.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed.jpg
```

### 從網頁檢查
```
https://contentcredentials.org/verify
```

### 常見 Manifest 範本
```json
{
  "claim_generator": "app-name/version",
  "assertions": [
    {
      "label": "stds.schema-org.CreativeWork",
      "data": {
        "author": [{"name": "Creator Name"}]
      }
    }
  ]
}
```

---

## 疑難排解

### 「找不到 C2PA 資料」
- 檔案可能沒有 C2PA manifest
- 中繼資料可能已被剝離
- 嘗試不同的檔案格式

### 「簽章無效」
- 簽署後檔案已修改
- 憑證已撤銷或過期
- 信任鏈中斷

### 「憑證不受信任」
- 使用自簽憑證(測試預期)
- CA 不在信任清單中
- 如有需要,新增自訂信任錨點

### 效能問題
- C2PA 每個 manifest 新增約 10-50KB(最少)
- 一般檔案簽署耗時 <1 秒
- 驗證幾乎是即時的

---

**準備好開始了嗎?**從上面選擇您的方法並深入探索!

**有問題嗎?**查看 [FAQ](faq.md) 或[開啟問題](https://github.com/paulortiz199928/awesome-c2pa/issues)。

---

*最後更新:2025 年 11 月*
