# Awesome C2PA [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> 다국어 규격, 도구, 라이브러리 및 학습 자료를 포함한 C2PA(Coalition for Content Provenance and Authenticity) 리소스 모음입니다.

**[English](../../README.md) | [简体中文](../zh-Hans/README.md) | [繁體中文](../zh-Hant/README.md) | [日本語](../ja/README.md) | 한국어 | [Deutsch](../de/README.md) | [Français](../fr/README.md) | [Русский](../ru/README.md)**

C2PA는 게시자, 크리에이터 및 소비자가 다양한 유형의 미디어 출처를 추적할 수 있는 개방형 기술 표준입니다. AI 생성 콘텐츠의 시대에 C2PA는 콘텐츠의 진위성과 출처를 검증하는 데 도움이 됩니다.

## 🌟 주요 특징

**🌍 다국어 공식 규격** - 본 프로젝트는 전 세계 개발자가 C2PA에 접근할 수 있도록 공식 C2PA 규격의 커뮤니티 주도 다국어 번역을 최초로 제공합니다.

**🤝 번역 개선에 참여하기** - 우리의 번역은 AI 지원(DeepL)을 받아 베타 단계에 있습니다. 원어민 여러분: 품질 개선을 위해 [오류를 보고](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md)해 주세요!

## 목차

- [공식 규격 (다국어)](#-공식-규격-다국어)
- [C2PA란 무엇인가?](#-c2pa란-무엇인가)
- [자주 묻는 질문](#-자주-묻는-질문)
- [공식 리소스](#-공식-리소스)
- [도구 및 라이브러리](#-도구-및-라이브러리)
  - [Rust](#rust)
  - [JavaScript/TypeScript](#javascripttypescript)
  - [Python](#python)
  - [Go](#go)
  - [Java](#java)
  - [기타 언어](#기타-언어)
- [명령줄 도구](#-명령줄-도구)
- [브라우저 확장 프로그램 및 애플리케이션](#-애플리케이션)
- [학습 자료](#-학습-자료)
  - [튜토리얼](#튜토리얼)
  - [비디오](#비디오)
  - [기사 및 블로그](#기사-및-블로그)
- [사용 사례 및 데모](#-사용-사례-및-데모)
- [조직 및 생태계](#-조직-및-생태계)
- [뉴스 및 업데이트](#-뉴스-및-업데이트)
- [커뮤니티](#-커뮤니티)
- [기여하기](#-기여하기)

---

## 🌍 공식 규격 (다국어)

C2PA 규격 버전 2.2는 여러 언어로 제공됩니다. 이러한 번역은 전 세계 개발자가 애플리케이션에서 C2PA를 이해하고 구현하는 데 도움이 됩니다.

| 언어 | 문서 | 상태 | 방법 | 최종 업데이트 |
|----------|----------|--------|--------|--------------|
| 🇬🇧 English | [C2PA Specification 2.2](../../docs/specifications/C2PA_Specification.pdf) | ✅ 공식 | C2PA Org | 2025년 5월 |
| 🇨🇳 简体中文 | [C2PA 规范 2.2](../../docs/specifications/C2PA_Specification_zh-Hans.pdf) | 🔄 베타 | AI + 검토 | 2025년 |
| 🇯🇵 日本語 | [C2PA 仕様 2.2](../../docs/specifications/C2PA_Specification_ja.pdf) | 🔄 베타 | AI + 검토 | 2025년 |
| 🇩🇪 Deutsch | [C2PA Spezifikation 2.2](../../docs/specifications/C2PA_Specification_de.pdf) | 🔄 베타 | AI + 검토 | 2025년 |
| 🇫🇷 Français | [Spécification C2PA 2.2](../../docs/specifications/C2PA_Specification_fr.pdf) | 🔄 베타 | AI + 검토 | 2025년 |
| 🇰🇷 한국어 | [C2PA 사양 2.2](docs/specifications/C2PA_Specification.pdf) | 🔄 베타 | AI + 검토 | 2025년 |
| 🇪🇸 Español | 곧 출시 예정 | 🚧 계획됨 | - | - |
| 🇵🇹 Português | 곧 출시 예정 | 🚧 계획됨 | - | - |

> **번역 안내**: 영어 이외의 번역은 커뮤니티 검토와 함께 AI 지원(DeepL)을 받습니다. 정확성을 위해 노력하고 있지만 오류가 있을 수 있습니다. 원어민께서는 [문제를 보고](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md)하거나 수정 사항을 제출해 주시기 바랍니다. 영어 버전이 공식 참조 문서입니다.

**빠른 탐색**: [모든 규격 보기 →](../../docs/README.md)

---

## 🤔 C2PA란 무엇인가?

**C2PA(Coalition for Content Provenance and Authenticity)**는 미디어 파일에 암호화 서명된 메타데이터를 추가하여 콘텐츠의 출처와 편집 기록을 검증할 수 있는 개방형 표준입니다.

**주요 이점:**
- ✅ 콘텐츠 진위성 검증 및 변조 탐지
- ✅ 원본에서 현재 버전까지의 완전한 편집 기록 추적
- ✅ AI 생성 또는 AI 수정 콘텐츠 식별
- ✅ 크리에이터 귀속 및 지적 재산 보호

**더 깊이 알아보고 싶으신가요?**
- 📖 [5분 빠른 시작 가이드](quick-start.md) - 즉시 실습하기
- ❓ [전체 FAQ](faq.md) - 25개 이상의 상세한 질문에 대한 답변
- 📚 [기술 규격](../../docs/README.md) - 표준에 대한 심층 분석

---

## ❓ 자주 묻는 질문

가장 일반적인 질문에 대한 빠른 답변:

<details>
<summary><b>C2PA란 무엇이며 어떻게 작동하나요?</b></summary>

C2PA는 출처 정보가 포함된 암호화 서명된 메타데이터("매니페스트(manifest)")를 미디어 파일에 추가합니다. 변조가 발생하면 서명이 깨져 수정 사항을 탐지할 수 있습니다. 블록체인이 아닌 표준 PKI(HTTPS 인증서와 같은)를 사용합니다.
</details>

<details>
<summary><b>C2PA를 제거할 수 있나요? AI 생성 이미지를 탐지할 수 있나요?</b></summary>

**제거**: 예, 설계상 가능합니다. C2PA는 제거를 방지하기보다는 *존재할 때* 진위성을 증명합니다.

**AI 탐지**: 자동으로는 아닙니다. C2PA는 크리에이터가 선언한 내용을 기록합니다. AI 도구는 매니페스트에 출력물을 "AI 생성"으로 자발적으로 라벨링해야 합니다.
</details>

<details>
<summary><b>어떤 카메라와 소프트웨어가 C2PA를 지원하나요?</b></summary>

**카메라**: Leica(M11-P, SL3), Sony(Alpha 1, A9 III, A7S III, A7 IV), Nikon(2025년 Z6 III 계획)은 촬영 시 사진에 서명할 수 있습니다.

**소프트웨어**: Adobe Photoshop/Lightroom, Capture One 및 많은 오픈소스 도구.

**비용**: 표준 및 도구는 무료입니다. 인증서 비용: 연간 약 $50-500.
</details>

**[→ 전체 25개 이상의 FAQ 보기](faq.md)** - 기술 세부 사항, 개인정보 보호, 보안 및 채택에 대한 내용을 다룹니다.

---

## 📚 공식 리소스

- [C2PA 공식 웹사이트](https://c2pa.org/) - 뉴스 및 정보가 있는 메인 웹사이트
- [C2PA 규격](https://c2pa.org/specifications/specifications/2.2/index.html) - 공식 규격 포털(v2.2)
- [C2PA GitHub 조직](https://github.com/c2pa-org) - 공식 GitHub 리포지토리
- [Content Authenticity Initiative](https://contentauthenticity.org/) - C2PA를 지원하는 Adobe 주도 이니셔티브

---

## 🛠️ 도구 및 라이브러리

### Rust

- [c2pa-rs](https://github.com/contentauth/c2pa-rs) - C2PA 매니페스트를 생성하고 검증하기 위한 공식 Rust SDK. 참조 구현입니다.

### JavaScript/TypeScript

- [c2pa-node-v2](https://github.com/contentauth/c2pa-node-v2) - C2PA Rust SDK를 위한 공식 Node.js 바인딩
- [c2pa-js](https://github.com/contentauth/c2pa-js) - 브라우저에서 C2PA 매니페스트를 읽기 위한 JavaScript 라이브러리

### Python

- [c2pa-python](https://github.com/contentauth/c2pa-python) - C2PA Rust SDK를 위한 공식 Python 바인딩

### Java

- [c2pa-java](https://github.com/contentauth/c2pa-java) - C2PA SDK를 위한 Java 바인딩

### 기타 언어

- [c2pa-c](https://github.com/contentauth/c2pa-c) - C2PA를 위한 C 및 C++ 바인딩
- [c2pa-ios](https://github.com/contentauth/c2pa-ios) - iOS용 C2PA SDK
- 언어 바인딩이 확장되고 있습니다 - 업데이트는 [공식 GitHub](https://github.com/contentauth/)에서 확인하세요

---

## 🔧 명령줄 도구

- [C2PA 명령줄 도구](https://github.com/contentauth/c2pa-rs/tree/main/cli) - C2PA 매니페스트 생성 및 검사를 위한 공식 명령줄 도구
  - C2PA 콘텐츠 생성, 읽기 및 검증
  - 크로스 플랫폼: Windows, macOS, Linux
  - 이미지, 비디오, 오디오 지원

---

## 🌐 애플리케이션

- [Content Credentials Verify](https://contentcredentials.org/verify) - C2PA 콘텐츠 검증을 위한 공식 웹 도구
---

## 📖 학습 자료

### 튜토리얼

- [C2PA 빠른 시작 가이드](quick-start.md) - C2PA 구현에 대한 5분 소개
- [C2PA 개발자 문서](https://opensource.contentauthenticity.org/docs) - 공식 시작 가이드 및 문서
- [C2PA 개발자 튜토리얼](https://opensource.contentauthenticity.org/docs/getting-started) - 단계별 구현 튜토리얼

### 비디오

- [Content Authenticity Initiative 소개](https://www.youtube.com/@contentauthenticity) - 교육 비디오가 있는 공식 YouTube 채널
- [C2PA 기술 개요](https://www.youtube.com/results?search_query=c2pa+technical) - 컨퍼런스 강연 및 기술 프레젠테이션
- [Content Credentials의 작동 방식](https://contentauthenticity.org/how-it-works) - 실제 C2PA에 대한 시각적 설명

### 기사 및 블로그

- [C2PA 공식 웹사이트](https://c2pa.org) - 뉴스, 업데이트 및 기술 리소스
- [Adobe Content Authenticity 블로그](https://blog.adobe.com/en/topics/content-authenticity) - 산업 인사이트 및 사용 사례
- [C2PA 매니페스트 이해하기](https://opensource.contentauthenticity.org/docs/manifest) - 기술 심층 분석

---

## 🎯 사용 사례 및 데모

### 산업 응용

- **뉴스 및 저널리즘**: 사진 및 비디오 진위성 검증(BBC, Reuters 시범 운영)
- **카메라 제조업체**: 카메라 내 C2PA 서명(Leica, Nikon, Sony)
- **소셜 미디어**: 플랫폼의 콘텐츠 출처(탐색 중)
- **AI 이미지 생성기**: AI 생성 콘텐츠 라벨링(Midjourney, DALL-E)
- **스톡 사진**: 원본 저작권 증명(Adobe Stock, Shutterstock)


## 🏢 조직 및 생태계

### 운영위원회 회원

- Adobe
- Arm
- BBC
- Intel
- Microsoft
- Publicis Groupe
- Sony
- Truepic

### 채택자 및 파트너

- **GenAI 제공업체**: [OpenAI](https://openai.com/index/understanding-the-source-of-what-we-see-and-hear-online/), [Google](https://blog.google/technology/ai/google-gen-ai-content-transparency-c2pa/), [Meta](https://about.fb.com/news/2024/02/labeling-ai-generated-images-on-facebook-instagram-and-threads)
- **카메라 제조업체**: Leica, Nikon, Sony, Canon
- **소프트웨어 회사**: Adobe, Microsoft, Capture One
- **뉴스 조직**: BBC, New York Times, Reuters
- **소셜 플랫폼**: 통합 탐색 중
- **인증 기관**: DigiCert, GlobalSign 등

---

## 📰 뉴스 및 업데이트

- [C2PA v2.2 규격 릴리스](https://c2pa.org) - 최신 버전(2025년)
- [Content Authenticity Initiative 마일스톤](https://contentauthenticity.org/news) - 산업 채택 업데이트
- [X/Twitter의 C2PA](https://twitter.com/C2PA_Coalition) - 실시간 업데이트 팔로우

---

## 🤝 커뮤니티

### 참여하기
- [Awesome C2PA GitHub 이슈](https://github.com/paulortiz199928/awesome-c2pa/issues) - 질문하고 아이디어 공유하기

### 이 프로젝트에 기여하기

기여를 환영합니다! 자세한 내용은 [기여 가이드](../../CONTRIBUTING.md)를 참조하세요:
- 새로운 리소스 추가
- 규격 번역
- 문서 개선
- 문제 보고

---

## 📋 기여하기

기여를 환영합니다! 먼저 [기여 가이드라인](../../CONTRIBUTING.md)을 읽어주세요.

### 기여 방법

1. **리소스 추가**: 새로운 도구, 라이브러리 또는 기사와 함께 PR 제출
2. **규격 번역**: C2PA 규격을 새로운 언어로 번역하도록 도와주세요
3. **오류 수정**: 번역 오류, 깨진 링크 또는 오래된 정보 보고 또는 수정
4. **콘텐츠 개선**: 설명 향상, 예제 추가 또는 섹션 재구성

### 품질 기준

다음과 같은 리소스를 수용합니다:
- 활발히 유지 관리됨(지난 1년 이내 업데이트)
- 잘 문서화됨
- C2PA 구현 또는 이해와 관련됨
- 오픈 소스(선호) 또는 자유롭게 액세스 가능

---

## 🙏 감사의 말

- 개방형 표준을 개발한 [C2PA 조직](https://c2pa.org)에 감사드립니다
- 채택을 촉진하는 [Content Authenticity Initiative](https://contentauthenticity.org)에 감사드립니다
- 이 리소스를 유지 관리하는 데 도움을 주는 모든 기여자에게 감사드립니다

---

**[⬆ 맨 위로](#목차)**

*최종 업데이트: 2025년 11월 | 커뮤니티에서 유지 관리*
