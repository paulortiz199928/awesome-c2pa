# C2PA 快速入门指南

5 分钟开始使用 C2PA！本指南将帮助您理解、验证和创建 C2PA 签名内容。

## 📋 目录

1. [理解 C2PA](#理解-c2pa)
2. [验证 C2PA 内容](#验证-c2pa-内容)
3. [创建 C2PA 内容](#创建-c2pa-内容)
4. [下一步](#下一步)

---

## 理解 C2PA

### 您需要了解的内容

**C2PA** 向您的媒体文件添加加密签名的"清单"，包含：
- **谁**：创作者/编辑者身份
- **什么**：执行的操作（创建、编辑、AI 生成）
- **何时**：时间戳
- **如何**：使用的工具和设置
- **来自**：源材料（成分）

### 30 秒理解关键概念

```
原始照片 → [添加 C2PA 清单] → 签名照片
                     ↓
              包含元数据：
              • 创作者：张三
              • 相机：Nikon Z9
              • 日期：2025-11-21
              • GPS：37.7749°N, 122.4194°W
              • 签名：✓ 有效
```

编辑时：
```
签名照片 → [在 Photoshop 中编辑] → 新签名照片
                                          ↓
                                   新清单引用
                                   原始作为"成分"
```

**结果**：从原始到当前版本的完整来源链。

---

## 验证 C2PA 内容

### 方法 1：在线工具（最简单）

**无需安装！**

1. 访问 https://contentcredentials.org/verify
2. 拖放任何图像/视频/文档
3. 查看来源信息：
   - 创作者身份
   - 编辑历史
   - 签名状态
   - 原始内容（如果可用）

**立即尝试** 示例图像：https://contentauthenticity.org/examples

### 方法 2：浏览器扩展

**在浏览时自动验证：**

1. 安装[内容凭证扩展](https://chrome.google.com/webstore)
   - 适用于 Chrome、Edge、Brave
2. 正常浏览
3. 扩展自动检测 C2PA 内容
4. 点击图标查看来源详情

### 方法 3：命令行

**对于开发者和高级用户：**

#### 安装 c2patool

```bash
# macOS/Linux（使用 Cargo）
cargo install c2patool

# macOS（使用 Homebrew）
brew install c2patool

# Windows
# 从以下位置下载：https://github.com/contentauth/c2patool/releases
```

#### 验证文件

```bash
# 基本验证
c2patool photo.jpg

# 详细 JSON 输出
c2patool photo.jpg --detailed

# 将清单保存到 JSON 文件
c2patool photo.jpg --output manifest.json

# 检查多个文件
c2patool *.jpg
```

#### 示例输出

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

### 方法 4：编程方式

**将验证集成到您的应用：**

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

## 创建 C2PA 内容

### 方法 1：使用支持的软件

**无需编码：**

#### Adobe Photoshop/Lightroom

1. 在 Photoshop/Lightroom 中打开图像
2. 转到**编辑 → 内容凭证**
3. 填写创作者信息
4. 保存文件 → 自动添加 C2PA 清单

#### 内置 C2PA 的相机

- **Nikon Z6 III**：在相机设置中启用（2025 年计划） → 拍摄时签名照片
- **Leica M11-P/SL3**：自动启用签名
- **Sony Alpha 系列**：通过固件更新启用

### 方法 2：命令行（c2patool）

#### 先决条件

您需要签名证书：

**用于测试（自签名）：**
```bash
# 生成测试证书（验证器不信任）
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes
```

**用于生产：**
- 从受信任的 CA 购买证书（DigiCert、GlobalSign 等）
- 指定 C2PA 密钥使用要求

#### 创建清单

创建 `manifest.json`：

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
            "name": "张三"
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

#### 签名文件

```bash
# 使用您的证书签名
c2patool photo.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed_photo.jpg

# 验证是否成功
c2patool signed_photo.jpg
```

### 方法 3：编程方式

#### Rust

```rust
use c2pa::{Builder, SigningAlg};

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let mut builder = Builder::from_file("input.jpg")?;

    // 添加创作者断言
    builder.add_assertion("stds.schema-org.CreativeWork",
        r#"{"author": [{"name": "张三"}]}"#)?;

    // 签名并保存
    let signer = get_signer(); // 您的证书/密钥
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
          author: [{ name: '张三' }]
        }
      }
    ]
  };

  const signer = {
    cert: 'path/to/cert.pem',
    key: 'path/to/key.pem'
  };

  await c2pa.sign(inputPath, outputPath, manifest, signer);
  console.log('签名成功！');
}

sign('input.jpg', 'output.jpg');
```

#### Python

```python
from c2pa import Builder, Signer

# 创建构建器
builder = Builder.from_file('input.jpg')

# 添加断言
builder.add_assertion('stds.schema-org.CreativeWork', {
    'author': [{'name': '张三'}]
})

# 签名
signer = Signer('cert.pem', 'key.pem')
builder.sign('output.jpg', signer)

print('签名成功！')
```

### 方法 4：编辑签名内容（保留来源）

编辑 C2PA 签名内容时，将原始内容引用为"成分"：

```bash
# 编辑并保留链
c2patool edited_photo.jpg \
  --parent original_photo.jpg \
  --manifest edit_manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output final_photo.jpg
```

新清单将引用 `original_photo.jpg` 作为成分，保留完整历史。

---

## 下一步

### 了解更多

**理解规范：**
- [英语](specifications/C2PA_Specification.pdf)
- [中文](specifications/C2PA_Specification_zh-Hans.pdf)
- [日本語](specifications/C2PA_Specification_ja.pdf)
- [Deutsch](specifications/C2PA_Specification_de.pdf)

**探索工具：**
- [工具和库](../README_zh-Hans.md#工具和库) - 所有主要语言的 SDK
- [官方文档](https://opensource.contentauthenticity.org/docs)

**常见问题：**
- [FAQ](FAQ_zh-Hans.md) - 25+ 个常见问题
- [GitHub 讨论](https://github.com/c2pa-org/specifications/discussions)

### 教程和示例

**官方教程：**
- [C2PA 开发者教程](https://opensource.contentauthenticity.org/docs/tutorial)
- [创建清单](https://opensource.contentauthenticity.org/docs/manifest/guide)
- [断言参考](https://opensource.contentauthenticity.org/docs/manifest/assertions)

**代码示例：**
- [c2pa-rs 示例](https://github.com/contentauth/c2pa-rs/tree/main/sdk/examples)
- [c2pa-node 示例](https://github.com/contentauth/c2pa-node/tree/main/examples)
- [c2pa-python 示例](https://github.com/contentauth/c2pa-python/tree/main/examples)

### 生产部署

**上线前：**

1. **获取生产证书**
   - 从受信任的 CA 购买（DigiCert、GlobalSign 等）
   - 确保 C2PA 兼容的密钥使用
   - 成本：约 50-500 美元/年

2. **安全密钥存储**
   - 为私钥使用硬件安全模块（HSM）
   - 或云 HSM（AWS CloudHSM、Azure Key Vault）
   - 切勿将密钥提交到源代码管理

3. **彻底测试**
   - 使用多个验证器验证签名
   - 测试不同文件格式
   - 检查跨平台兼容性

4. **监控和维护**
   - 实施证书轮换
   - 监控撤销
   - 保持 SDK 更新

### 与您的应用集成

**关键集成点：**

```
您的应用工作流：

1. 内容创建/上传
   ↓
2. [添加 C2PA 清单] ← 您的集成点
   ↓
3. 使用证书签名
   ↓
4. 保存/发布签名内容
   ↓
5. [可选] 显示时验证 ← 另一个集成点
```

**典型集成时间：**
- 简单验证：1-2 天
- 基本签名：3-5 天
- 完整生产部署：2-4 周

### 获取证书

**测试（免费）：**
- 自签名证书
- 仅适用于开发
- 验证器不信任

**生产：**
- **DigiCert**：https://www.digicert.com/
- **GlobalSign**：https://www.globalsign.com/
- **Entrust**：https://www.entrust.com/
- 请求带有 C2PA 密钥使用扩展的证书

### 加入社区

**获取帮助：**
- [GitHub Issues](https://github.com/c2pa-org/specifications/issues) - 错误报告
- [GitHub 讨论](https://github.com/c2pa-org/specifications/discussions) - 问题
- [C2PA 网站](https://c2pa.org) - 官方资源

**贡献：**
- [awesome-c2pa](../README_zh-Hans.md) - 添加资源、翻译文档
- [C2PA 实现](https://github.com/contentauth) - 贡献代码
- [内容真实性倡议](https://contentauthenticity.org) - 加入运动

---

## 快速参考卡

### 验证内容
```bash
c2patool image.jpg
```

### 签名内容
```bash
c2patool input.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed.jpg
```

### 从 Web 检查
```
https://contentcredentials.org/verify
```

### 常见清单模板
```json
{
  "claim_generator": "app-name/version",
  "assertions": [
    {
      "label": "stds.schema-org.CreativeWork",
      "data": {
        "author": [{"name": "创作者姓名"}]
      }
    }
  ]
}
```

---

## 故障排除

### "未找到 C2PA 数据"
- 文件可能没有 C2PA 清单
- 元数据可能已被删除
- 尝试不同的文件格式

### "无效签名"
- 签名后文件被修改
- 证书被撤销或过期
- 信任链断开

### "证书不受信任"
- 使用自签名证书（测试预期）
- CA 不在信任列表中
- 如果需要，添加自定义信任锚点

### 性能问题
- C2PA 每个清单添加约 10-50KB（最小）
- 典型文件签名时间 < 1 秒
- 验证几乎是即时的

---

**准备好开始了吗？** 选择上面的方法并开始！

**有问题？** 查看 [FAQ](FAQ_zh-Hans.md) 或[提交 issue](https://github.com/paulortiz199928/awesome-c2pa/issues)。

---

*最后更新：2025 年 11 月*
