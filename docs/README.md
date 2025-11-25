# C2PA Specification - Multi-language Documentation

**📍 Navigation:** [← Main](../README.md) | [Quick Start →](guides/quick-start.md) | [FAQ →](guides/faq.md)

This directory contains the official C2PA (Coalition for Content Provenance and Authenticity) specification version 2.2 in multiple languages.

> ⚠️ **Translation Quality Notice**: Non-English translations are AI-assisted (DeepL) and are currently in **beta** status. Technical terminology may contain inaccuracies. Native speakers are strongly encouraged to review and report errors. The English version is the authoritative reference for all technical implementations.

## 📖 Available Specifications

### English (Official)
- **File**: [C2PA_Specification.pdf](specifications/C2PA_Specification.pdf)
- **Source**: [C2PA Organization](https://c2pa.org)
- **Version**: 2.2
- **Status**: ✅ Official Release

### 简体中文 (Simplified Chinese)
- **File**: [C2PA_Specification_zh-Hans.pdf](specifications/C2PA_Specification_zh-Hans.pdf)
- **Translation Status**: 🔄 Beta (AI-assisted, needs native review)
- **Translation Method**: DeepL + community review
- **Version**: 2.2
- **Last Updated**: 2025

### 日本語 (Japanese)
- **File**: [C2PA_Specification_ja.pdf](specifications/C2PA_Specification_ja.pdf)
- **Translation Status**: 🔄 Beta (AI-assisted, needs native review)
- **Translation Method**: DeepL + community review
- **Version**: 2.2
- **Last Updated**: 2025

### Deutsch (German)
- **File**: [C2PA_Specification_de.pdf](specifications/C2PA_Specification_de.pdf)
- **Translation Status**: 🔄 Beta (AI-assisted, needs native review)
- **Translation Method**: DeepL + community review
- **Version**: 2.2
- **Last Updated**: 2025

### Français (French)
- **File**: [C2PA_Specification_fr.pdf](specifications/C2PA_Specification_fr.pdf)
- **Translation Status**: 🔄 Beta (AI-assisted, needs native review)
- **Translation Method**: DeepL + community review
- **Version**: 2.2
- **Last Updated**: 2025

## 🚧 Planned Translations

We are planning to add the following language translations:

- 🇰🇷 **한국어 (Korean)** - Seeking translators
- 🇪🇸 **Español (Spanish)** - Seeking translators
- 🇵🇹 **Português (Portuguese)** - Seeking translators

## 📋 Specification Overview

The C2PA specification defines:

1. **Manifest Format** - Structure of C2PA manifests embedded in media files
2. **Assertion Types** - Standard claims about content (authorship, edits, AI usage, etc.)
3. **Signature Mechanisms** - Cryptographic signing for tamper detection
4. **Trust Model** - Certificate authorities and validation chains
5. **Media Format Bindings** - How to embed manifests in JPEG, PNG, MP4, PDF, etc.

## 🗂️ Specification Sections

The specification is organized into the following major sections:

### Part 1: Introduction
- What is C2PA?
- Use cases and scenarios
- Key concepts and terminology

### Part 2: Manifest Structure
- Manifest format and encoding
- Claims and assertions
- Relationship between manifests

### Part 3: Cryptographic Security
- Digital signatures
- Hash functions
- Certificate requirements

### Part 4: Media Format Integration
- Image formats (JPEG, PNG, WebP, AVIF, HEIC)
- Video formats (MP4, MOV)
- Audio formats (WAV, MP3)
- Document formats (PDF)

### Part 5: Trust and Validation
- Trust anchors and certificate authorities
- Validation algorithms
- Error handling

## 🔍 Quick Reference

### Key Concepts

| Concept | Description |
|---------|-------------|
| **Manifest** | A JSON-based structure containing all C2PA metadata |
| **Assertion** | A specific claim about the content (e.g., "edited with Photoshop") |
| **Ingredient** | A reference to source content used to create the current content |
| **Claim** | The core data structure binding assertions together |
| **Signature** | Cryptographic proof of authenticity |

### Common Assertion Types

| Assertion | Purpose |
|-----------|---------|
| `c2pa.actions` | Records editing actions performed on content |
| `c2pa.hash.data` | Cryptographic hash of the asset |
| `stds.schema-org.CreativeWork` | Creator attribution metadata |
| `c2pa.thumbnail.claim.jpeg` | Visual thumbnail of the content |
| `c2pa.ingredient` | Reference to source materials |

## 📚 Related Documentation

- [C2PA Official Website](https://c2pa.org/)
- [C2PA GitHub Repository](https://github.com/c2pa-org/specifications)
- [Content Authenticity Initiative](https://contentauthenticity.org/)
- [Open Source Implementation Docs](https://opensource.contentauthenticity.org/)

## 🤝 Translation Guidelines

### How to Contribute Translations

If you'd like to contribute a translation:

1. **Check for existing work**: Look at our [issues](../../issues) to see if someone is already working on your language
2. **Announce your intent**: Open an issue to let others know you're working on a translation
3. **Translation process**:
   - Maintain technical accuracy - key terms should remain consistent
   - Preserve all diagrams and code examples
   - Keep the document structure identical to the original
   - Add a translation note on the title page
4. **Submit for review**: Open a pull request with your completed translation

### Translation Quality Standards

- **Technical Accuracy**: All technical terms must be correctly translated
- **Consistency**: Use consistent terminology throughout (create a glossary)
- **Completeness**: Translate all sections including diagrams and examples
- **Formatting**: Preserve original document structure and formatting
- **Review**: Have at least one other native speaker review the translation

### Key Terms Glossary

| English | 中文 | 日本語 | Deutsch | Français |
|---------|------|--------|---------|----------|
| Manifest | 清单 | マニフェスト | Manifest | Manifeste |
| Assertion | 断言 | アサーション | Assertion | Assertion |
| Provenance | 来源 | プロヴェナンス | Herkunft | Provenance |
| Claim | 声明 | クレーム | Anspruch | Revendication |
| Ingredient | 成分 | 素材 | Zutat | Ingrédient |
| Signature | 签名 | 署名 | Signatur | Signature |

## 🔍 Translation Quality & Improvement

### Current Status

All non-English translations are **AI-assisted (DeepL)** and in **beta** status. We acknowledge that:

- ✅ **Strengths**: General meaning and structure are preserved
- ⚠️ **Known Issues**:
  - Technical terminology may be inconsistent or inaccurate
  - Context-specific terms may be mistranslated
  - Cultural idioms may not translate well
  - Formatting artifacts may exist

### How You Can Help

We **actively seek native speakers** to improve translation quality:

1. **Report Errors**: [Open a translation issue](../../issues/new?template=translation.md)
   - Specify: Language, page number, incorrect text, suggested correction
   - Even small corrections help!

2. **Review Sections**:
   - Focus on technical terminology (Manifest, Assertion, Claim, etc.)
   - Verify code examples and technical descriptions
   - Check consistency across document

3. **Become a Reviewer**:
   - Native speakers with C2PA knowledge are especially valuable
   - Contact us via Issues to coordinate review efforts

### Quality Improvement Roadmap

**Phase 1** (Current): AI-translated beta versions available
**Phase 2** (Next): Native speaker review of technical terms
**Phase 3** (Goal): Community-verified translations marked as "Reviewed"

### Version Priority

- **For Reading/Learning**: Translated versions provide good general understanding
- **For Implementation**: Always refer to English version for technical accuracy
- **When in Doubt**: English version is authoritative

## ⚠️ Important Notes

- **Official Source**: The English version is the authoritative specification. In case of discrepancies, the English version takes precedence.
- **Version Tracking**: Always check that you're reading the correct version (currently 2.2)
- **Translation Method**: Translations use DeepL AI with ongoing community review

## 📮 Feedback and Corrections

Found an error in a translation? Have suggestions for improvement?

- **Report Issues**: [Open an issue](../../issues/new)
- **Discuss**: Use [GitHub Discussions](../../discussions)
- **Contribute**: Submit a pull request with corrections

## 📄 License

The C2PA specification is available under the [C2PA Specification License](https://c2pa.org/specifications/specifications/2.2/index.html#_license).

Community translations in this repository are provided under the same license terms.

---

**[← Back to Main README](../README.md)**