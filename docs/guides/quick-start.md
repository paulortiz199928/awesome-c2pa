# C2PA Quick Start Guide

Get started with C2PA in 5 minutes! This guide will help you understand, verify, and create C2PA-signed content.

## 📋 Table of Contents

1. [Understanding C2PA](#understanding-c2pa)
2. [Verifying C2PA Content](#verifying-c2pa-content)
3. [Creating C2PA Content](#creating-c2pa-content)
4. [Next Steps](#next-steps)

---

## Understanding C2PA

### What You Need to Know

**C2PA** adds a cryptographically signed "manifest" to your media files containing:
- **Who**: Creator/editor identity
- **What**: Actions performed (created, edited, AI-generated)
- **When**: Timestamps
- **How**: Tools and settings used
- **From**: Source materials (ingredients)

### Key Concepts in 30 Seconds

```
Original Photo → [Add C2PA Manifest] → Signed Photo
                     ↓
              Contains metadata:
              • Creator: John Doe
              • Camera: Nikon Z9
              • Date: 2025-11-21
              • GPS: 37.7749°N, 122.4194°W
              • Signature: ✓ Valid
```

When you edit:
```
Signed Photo → [Edit in Photoshop] → New Signed Photo
                                          ↓
                                   New manifest references
                                   original as "ingredient"
```

**Result**: Complete provenance chain from original to current version.

---

## Verifying C2PA Content

### Method 1: Online Tool (Easiest)

**No installation required!**

1. **Visit the verification tool**: Open your web browser and navigate to https://contentcredentials.org/verify to access the official C2PA verification tool.

2. **Upload your media file**: Drag and drop your image, video, or document onto the verification page, or click to browse and select the file from your device.

3. **Review provenance information**: Examine the displayed information including:
   - Creator identity
   - Creation date
   - Editing history
   - Tools and software used

4. **Verify signature status**: Check that the signature shows as "Valid" with a green checkmark, confirming the content has not been tampered with since signing.

**Try it now** with sample images from: https://contentauthenticity.org/examples

### Method 2: Browser Extension

**For automatic verification while browsing:**

1. Install [Content Credentials Extension](https://chrome.google.com/webstore)
   - Available for Chrome, Edge, Brave
2. Browse normally
3. Extension automatically detects C2PA content
4. Click icon to view provenance details

### Method 3: Command Line

**For developers and power users:**

#### Install c2patool

```bash
# macOS/Linux (using Cargo)
cargo install c2patool

# macOS (using Homebrew)
brew install c2patool

# Windows
# Download from: https://github.com/contentauth/c2patool/releases
```

#### Verify a File

```bash
# Basic verification
c2patool photo.jpg

# Detailed JSON output
c2patool photo.jpg --detailed

# Save manifest to JSON file
c2patool photo.jpg --output manifest.json

# Check multiple files
c2patool *.jpg
```

#### Example Output

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

### Method 4: Programmatically

**Integrate verification into your app:**

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

## Creating C2PA Content

### Method 1: Use Supported Software

**No coding required:**

#### Adobe Photoshop/Lightroom

1. Open image in Photoshop/Lightroom
2. Go to **Edit → Content Credentials**
3. Fill in creator information
4. Save file → C2PA manifest automatically added

#### Cameras with Built-in C2PA

- **Nikon Z9/Z8**: Enable in camera settings → photos signed at capture
- **Leica M11-P/SL3**: Automatic signing enabled
- **Sony Alpha series**: Enable via firmware update

### Method 2: Command Line (c2patool)

#### Prerequisites

You need a signing certificate:

**For Testing (Self-Signed):**
```bash
# Generate test certificate (not trusted by validators)
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes
```

**For Production:**
- Purchase certificate from trusted CA (DigiCert, GlobalSign, etc.)
- Specify C2PA key usage requirements

#### Create a Manifest

Create `manifest.json`:

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

#### Sign the File

```bash
# Sign with your certificate
c2patool photo.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed_photo.jpg

# Verify it worked
c2patool signed_photo.jpg
```

### Method 3: Programmatically

#### Rust

```rust
use c2pa::{Builder, SigningAlg};

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let mut builder = Builder::from_file("input.jpg")?;

    // Add creator assertion
    builder.add_assertion("stds.schema-org.CreativeWork",
        r#"{"author": [{"name": "John Doe"}]}"#)?;

    // Sign and save
    let signer = get_signer(); // Your certificate/key
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

# Create builder
builder = Builder.from_file('input.jpg')

# Add assertions
builder.add_assertion('stds.schema-org.CreativeWork', {
    'author': [{'name': 'John Doe'}]
})

# Sign
signer = Signer('cert.pem', 'key.pem')
builder.sign('output.jpg', signer)

print('Signed successfully!')
```

### Method 4: Editing Signed Content (Preserving Provenance)

When editing C2PA-signed content, reference the original as an "ingredient":

```bash
# Edit and preserve chain
c2patool edited_photo.jpg \
  --parent original_photo.jpg \
  --manifest edit_manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output final_photo.jpg
```

The new manifest will reference `original_photo.jpg` as an ingredient, preserving the complete history.

---

## Next Steps

### Learn More

**Understand the Specification:**
- [English](specifications/C2PA_Specification.pdf)
- [中文](specifications/C2PA_Specification_zh-Hans.pdf)
- [日本語](specifications/C2PA_Specification_ja.pdf)
- [Deutsch](specifications/C2PA_Specification_de.pdf)

**Explore Tools:**
- [Tools & Libraries](../../README.md#tools--libraries) - SDKs for all major languages
- [Official Documentation](https://opensource.contentauthenticity.org/docs)

**Common Questions:**
- [FAQ](faq.md) - 25+ frequently asked questions
- [GitHub Discussions](https://github.com/c2pa-org/specifications/discussions)

### Tutorials & Examples

**Official Tutorials:**
- [C2PA Developer Tutorial](https://opensource.contentauthenticity.org/docs/tutorial)
- [Creating Manifests](https://opensource.contentauthenticity.org/docs/manifest/guide)
- [Assertion Reference](https://opensource.contentauthenticity.org/docs/manifest/assertions)

**Code Examples:**
- [c2pa-rs Examples](https://github.com/contentauth/c2pa-rs/tree/main/sdk/examples)
- [c2pa-node Examples](https://github.com/contentauth/c2pa-node/tree/main/examples)
- [c2pa-python Examples](https://github.com/contentauth/c2pa-python/tree/main/examples)

### Production Deployment

**Before Going Live:**

1. **Get Production Certificate**
   - Purchase from trusted CA (DigiCert, GlobalSign, etc.)
   - Ensure C2PA-compatible key usage
   - Cost: ~$50-500/year

2. **Secure Key Storage**
   - Use Hardware Security Module (HSM) for private keys
   - Or cloud HSM (AWS CloudHSM, Azure Key Vault)
   - Never commit keys to source control

3. **Test Thoroughly**
   - Verify signatures with multiple validators
   - Test on different file formats
   - Check cross-platform compatibility

4. **Monitor & Maintain**
   - Implement certificate rotation
   - Monitor for revocations
   - Keep SDKs updated

### Integrating with Your Application

**Key Integration Points:**

```
Your App Workflow:

1. Content Creation/Upload
   ↓
2. [Add C2PA Manifest] ← Your integration point
   ↓
3. Sign with Certificate
   ↓
4. Save/Publish Signed Content
   ↓
5. [Optional] Verify on Display ← Another integration point
```

**Typical Integration Time:**
- Simple verification: 1-2 days
- Basic signing: 3-5 days
- Full production deployment: 2-4 weeks

### Get Certificates

**Testing (Free):**
- Self-signed certificates
- Good for development only
- Not trusted by validators

**Production:**
- **DigiCert**: https://www.digicert.com/
- **GlobalSign**: https://www.globalsign.com/
- **Entrust**: https://www.entrust.com/
- Request certificates with C2PA key usage extensions

### Join the Community

**Get Help:**
- [GitHub Issues](https://github.com/c2pa-org/specifications/issues) - Bug reports
- [GitHub Discussions](https://github.com/c2pa-org/specifications/discussions) - Questions
- [C2PA Website](https://c2pa.org) - Official resources

**Contribute:**
- [awesome-c2pa](../../README.md) - Add resources, translate docs
- [C2PA Implementations](https://github.com/contentauth) - Contribute code
- [Content Authenticity Initiative](https://contentauthenticity.org) - Join the movement

---

## Quick Reference Card

### Verify Content
```bash
c2patool image.jpg
```

### Sign Content
```bash
c2patool input.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed.jpg
```

### Check from Web
```
https://contentcredentials.org/verify
```

### Common Manifest Template
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

## Troubleshooting

### "No C2PA data found"
- File may not have C2PA manifest
- Metadata may have been stripped
- Try different file format

### "Invalid signature"
- File modified after signing
- Certificate revoked or expired
- Trust chain broken

### "Certificate not trusted"
- Using self-signed cert (expected for testing)
- CA not in trust list
- Add custom trust anchors if needed

### Performance Issues
- C2PA adds ~10-50KB per manifest (minimal)
- Signing takes <1 second for typical files
- Verification is nearly instant

---

**Ready to start?** Pick your method above and dive in!

**Questions?** Check the [FAQ](faq.md) or [open an issue](https://github.com/paulortiz199928/awesome-c2pa/issues).

---

*Last updated: November 2025