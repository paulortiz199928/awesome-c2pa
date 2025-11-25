# Awesome C2PA [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of C2PA (Coalition for Content Provenance and Authenticity) resources, including multi-language specifications, tools, libraries, and learning materials.

**English | [简体中文](i18n/zh-Hans/README.md) | [繁體中文](i18n/zh-Hant/README.md) | [日本語](i18n/ja/README.md) | [한국어](i18n/ko/README.md) | [Deutsch](i18n/de/README.md) | [Français](i18n/fr/README.md) | [Русский](i18n/ru/README.md)**

C2PA is an open technical standard providing publishers, creators, and consumers the ability to trace the origin of different types of media. In the age of AI-generated content, C2PA helps verify content authenticity and provenance.

## 🌟 Highlights

**🌍 Multi-language Official Specifications** - This project provides the first community-driven translations of the official C2PA specification in multiple languages, making C2PA accessible to developers worldwide.

**🤝 Help Improve Translations** - Our translations are AI-assisted (DeepL) and in beta. Native speakers: [report errors](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md) to help improve quality!

## Contents

- [Official Specifications (Multi-language)](#-official-specifications-multi-language)
- [What is C2PA?](#-what-is-c2pa)
- [Frequently Asked Questions](#-frequently-asked-questions)
- [Official Resources](#-official-resources)
- [Tools & Libraries](#-tools--libraries)
  - [Rust](#rust)
  - [JavaScript/TypeScript](#javascripttypescript)
  - [Python](#python)
  - [Go](#go)
  - [Java](#java)
  - [Other Languages](#other-languages)
- [Command Line Tools](#-command-line-tools)
- [Browser Extensions & Applications](#-browser-extensions--applications)
- [Learning Resources](#-learning-resources)
  - [Tutorials](#tutorials)
  - [Videos](#videos)
  - [Articles & Blogs](#articles--blogs)
- [Use Cases & Demos](#-use-cases--demos)
- [Organizations & Ecosystem](#-organizations--ecosystem)
- [News & Updates](#-news--updates)
- [Community](#-community)
- [Contributing](#-contributing)

---

## 🌍 Official Specifications (Multi-language)

The C2PA specification version 2.2 is available in multiple languages. These translations help developers worldwide understand and implement C2PA in their applications.

| Language | Document | Status | Method | Last Updated |
|----------|----------|--------|--------|--------------|
| 🇬🇧 English | [C2PA Specification 2.2](docs/specifications/C2PA_Specification.pdf) | ✅ Official | C2PA Org | May 2025 |
| 🇨🇳 简体中文 | [C2PA 规范 2.2](docs/specifications/C2PA_Specification_zh-Hans.pdf) | 🔄 Beta | AI + Review | 2025 |
| 🇯🇵 日本語 | [C2PA 仕様 2.2](docs/specifications/C2PA_Specification_ja.pdf) | 🔄 Beta | AI + Review | 2025 |
| 🇩🇪 Deutsch | [C2PA Spezifikation 2.2](docs/specifications/C2PA_Specification_de.pdf) | 🔄 Beta | AI + Review | 2025 |
| 🇫🇷 Français | [Spécification C2PA 2.2](docs/specifications/C2PA_Specification_fr.pdf) | 🔄 Beta | AI + Review | 2025 |
| 🇰🇷 한국어 | Coming soon | 🚧 Planned | - | - |
| 🇪🇸 Español | Coming soon | 🚧 Planned | - | - |
| 🇵🇹 Português | Coming soon | 🚧 Planned | - | - |

> **Translation Notice**: Non-English translations are AI-assisted (DeepL) with community review. While we strive for accuracy, errors may exist. Native speakers are encouraged to [report issues](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md) or submit corrections. The English version remains the authoritative reference.

**Quick Navigation**: [View all specifications →](docs/README.md)

---

## 🤔 What is C2PA?

**C2PA (Coalition for Content Provenance and Authenticity)** is an open standard that adds cryptographically signed metadata to media files, enabling verification of content origin and editing history.

**Key Benefits:**
- ✅ Verify content authenticity and detect tampering
- ✅ Track complete editing history from original to current version
- ✅ Identify AI-generated or AI-modified content
- ✅ Protect creator attribution and intellectual property

**Want to dive deeper?**
- 📖 [5-Minute Quick Start Guide](docs/guides/quick-start.md) - Get hands-on immediately
- ❓ [Complete FAQ](docs/guides/faq.md) - 25+ detailed questions answered
- 📚 [Technical Specifications](docs/README.md) - Deep dive into the standard

---

## ❓ Frequently Asked Questions

Quick answers to the most common questions:

<details>
<summary><b>What is C2PA and how does it work?</b></summary>

C2PA adds cryptographically signed metadata ("manifests") to media files containing provenance information. Any tampering breaks the signature, making modifications detectable. It uses standard PKI (like HTTPS certificates), not blockchain.
</details>

<details>
<summary><b>Can C2PA be removed? Can it detect AI-generated images?</b></summary>

**Removal**: Yes, by design. C2PA proves authenticity *when present*, rather than preventing removal.

**AI Detection**: Not automatically. C2PA records what creators declare. AI tools must voluntarily label their output as "AI-generated" in manifests.
</details>

<details>
<summary><b>Which cameras and software support C2PA?</b></summary>

**Cameras**: Leica (M11-P, SL3), Sony (Alpha 1, A9 III, A7S III, A7 IV), Nikon (Z6 III planned for 2025) can sign photos at capture time.

**Software**: Adobe Photoshop/Lightroom, Capture One, and many open-source tools.

**Cost**: The standard and tools are free. Certificate fees: ~$50-500/year.
</details>

**[→ View all 25+ FAQs](docs/guides/faq.md)** covering technical details, privacy, security, and adoption.

---

## 📚 Official Resources

- [C2PA Official Website](https://c2pa.org/) - Main website with news and information
- [C2PA Specifications](https://c2pa.org/specifications/specifications/2.2/index.html) - Official specification portal (v2.2)
- [C2PA GitHub Organization](https://github.com/c2pa-org) - Official GitHub repositories
- [Content Authenticity Initiative](https://contentauthenticity.org/) - Adobe-led initiative supporting C2PA

---

## 🛠️ Tools & Libraries

### Rust

- [c2pa-rs](https://github.com/contentauth/c2pa-rs) - Official Rust SDK for creating and validating C2PA manifests. The reference implementation.

### JavaScript/TypeScript

- [c2pa-node-v2](https://github.com/contentauth/c2pa-node-v2) - Official Node.js bindings for the C2PA Rust SDK
- [c2pa-js](https://github.com/contentauth/c2pa-js) - JavaScript library for reading C2PA manifests in browsers

### Python

- [c2pa-python](https://github.com/contentauth/c2pa-python) - Official Python bindings for the C2PA Rust SDK

### Java

- [c2pa-java](https://github.com/contentauth/c2pa-java) - Java bindings for the C2PA SDK

### Other Languages

- [c2pa-c](https://github.com/contentauth/c2pa-c) - C and C++ binding for C2PA 
- [c2pa-ios](https://github.com/contentauth/c2pa-ios) - C2PA SDK for iOS
- Language bindings are expanding - check the [official GitHub](https://github.com/contentauth/) for updates

---

## 🔧 Command Line Tools

- [C2PA command line tool](https://github.com/contentauth/c2pa-rs/tree/main/cli) - Official command-line tool for creating and inspecting C2PA manifests
  - Create, read, and validate C2PA content
  - Cross-platform: Windows, macOS, Linux
  - Supports images, videos, audio

---

## 🌐 Applications

- [Content Credentials Verify](https://contentcredentials.org/verify) - Official web tool for verifying C2PA content
---

## 📖 Learning Resources

### Tutorials

- [C2PA Quick Start Guide](docs/guides/quick-start.md) - 5-minute introduction to C2PA implementation
- [C2PA Developer Documentation](https://opensource.contentauthenticity.org/docs) - Official getting started guide and documentation
- [C2PA Developer Tutorial](https://opensource.contentauthenticity.org/docs/getting-started) - Step-by-step implementation tutorial

### Videos

- [Content Authenticity Initiative Introduction](https://www.youtube.com/@contentauthenticity) - Official YouTube channel with educational videos
- [C2PA Technical Overview](https://www.youtube.com/results?search_query=c2pa+technical) - Conference talks and technical presentations
- [How Content Credentials Work](https://contentauthenticity.org/how-it-works) - Visual explainer of C2PA in action

### Articles & Blogs

- [C2PA Official Website](https://c2pa.org) - News, updates, and technical resources
- [Adobe Content Authenticity Blog](https://blog.adobe.com/en/topics/content-authenticity) - Industry insights and use cases
- [Understanding C2PA Manifests](https://opensource.contentauthenticity.org/docs/manifest) - Technical deep dive

---

## 🎯 Use Cases & Demos

### Industry Applications

- **News & Journalism**: Verify photo and video authenticity (BBC, Reuters trials)
- **Camera Manufacturers**: In-camera C2PA signing (Leica, Nikon, Sony)
- **Social Media**: Content provenance on platforms (exploring)
- **AI Image Generators**: Labeling AI-generated content (Midjourney, DALL-E)
- **Stock Photography**: Proving original authorship (Adobe Stock, Shutterstock)


## 🏢 Organizations & Ecosystem

### Steering Committee Members

- Adobe
- Arm
- BBC
- Intel
- Microsoft
- Publicis Groupe
- Sony
- Truepic

### Adopters & Partners

- **GenAI Providers**: [OpenAI](https://openai.com/index/understanding-the-source-of-what-we-see-and-hear-online/), [Google](https://blog.google/technology/ai/google-gen-ai-content-transparency-c2pa/), [Meta](https://about.fb.com/news/2024/02/labeling-ai-generated-images-on-facebook-instagram-and-threads)
- **Camera Manufacturers**: Leica, Nikon, Sony, Canon
- **Software Companies**: Adobe, Microsoft, Capture One
- **News Organizations**: BBC, New York Times, Reuters
- **Social Platforms**: Exploring integration
- **Certification Authorities**: DigiCert, GlobalSign, and others

---

## 📰 News & Updates

- [C2PA v2.2 Specification Released](https://c2pa.org) - Latest version (2025)
- [Content Authenticity Initiative Milestones](https://contentauthenticity.org/news) - Industry adoption updates
- [C2PA on X/Twitter](https://twitter.com/C2PA_Coalition) - Follow for real-time updates

---

## 🤝 Community

### Get Involved
- [Awesome C2PA GitHub Issues](https://github.com/paulortiz199928/awesome-c2pa/issues) - Ask questions and share ideas

### Contribute to This Project

We welcome contributions! See our [Contributing Guide](CONTRIBUTING.md) for details on:
- Adding new resources
- Translating specifications
- Improving documentation
- Reporting issues

---

## 📋 Contributing

Contributions are welcome! Please read our [Contributing Guidelines](CONTRIBUTING.md) first.

### How to Contribute

1. **Adding Resources**: Submit a PR with new tools, libraries, or articles
2. **Translating Specs**: Help translate the C2PA specification to new languages
3. **Fixing Errors**: Report or fix translation errors, broken links, or outdated info
4. **Improving Content**: Enhance descriptions, add examples, or restructure sections

### Quality Standards

We accept resources that are:
- Actively maintained (updated within the last year)
- Well-documented
- Relevant to C2PA implementation or understanding
- Open source (preferred) or freely accessible

---

## 🙏 Acknowledgments

- Thanks to the [C2PA Organization](https://c2pa.org) for developing the open standard
- Thanks to the [Content Authenticity Initiative](https://contentauthenticity.org) for promoting adoption
- Thanks to all contributors who help maintain this resource

---

**[⬆ Back to Top](#contents)**

*Last Updated: November 2025 | Maintained by the community*
