# C2PA 빠른 시작 가이드

5분 안에 C2PA를 시작하세요! 이 가이드는 C2PA 서명 콘텐츠를 이해하고, 검증하고, 생성하는 데 도움이 됩니다.

## 📋 목차

1. [C2PA 이해하기](#c2pa-이해하기)
2. [C2PA 콘텐츠 검증](#c2pa-콘텐츠-검증)
3. [C2PA 콘텐츠 생성](#c2pa-콘텐츠-생성)
4. [다음 단계](#다음-단계)

---

## C2PA 이해하기

### 알아야 할 사항

**C2PA**는 다음을 포함하는 암호화 서명된 "매니페스트(manifest)"를 미디어 파일에 추가합니다:
- **누가**: 크리에이터/편집자 신원
- **무엇을**: 수행된 작업(생성됨, 편집됨, AI 생성됨)
- **언제**: 타임스탬프
- **어떻게**: 사용된 도구 및 설정
- **어디서**: 소스 자료(재료)

### 30초 만에 핵심 개념

```
원본 사진 → [C2PA 매니페스트 추가] → 서명된 사진
                     ↓
              메타데이터 포함:
              • 크리에이터: John Doe
              • 카메라: Nikon Z9
              • 날짜: 2025-11-21
              • GPS: 37.7749°N, 122.4194°W
              • 서명: ✓ 유효함
```

편집할 때:
```
서명된 사진 → [Photoshop에서 편집] → 새로 서명된 사진
                                          ↓
                                   새 매니페스트가 원본을
                                   "재료"로 참조
```

**결과**: 원본에서 현재 버전까지의 완전한 출처 체인.

---

## C2PA 콘텐츠 검증

### 방법 1: 온라인 도구 (가장 쉬움)

**설치 불필요!**

1. https://contentcredentials.org/verify 방문
2. 이미지/비디오/문서 드래그 앤 드롭
3. 출처 정보 보기:
   - 크리에이터 신원
   - 편집 기록
   - 서명 상태
   - 원본 콘텐츠(사용 가능한 경우)

**지금 시도해 보세요** 샘플 이미지: https://contentauthenticity.org/examples

### 방법 2: 브라우저 확장 프로그램

**브라우징 중 자동 검증:**

1. [Content Credentials 확장 프로그램](https://chrome.google.com/webstore) 설치
   - Chrome, Edge, Brave에서 사용 가능
2. 정상적으로 브라우징
3. 확장 프로그램이 C2PA 콘텐츠를 자동으로 탐지
4. 아이콘을 클릭하여 출처 세부 정보 보기

### 방법 3: 명령줄

**개발자 및 고급 사용자용:**

#### c2patool 설치

```bash
# macOS/Linux (Cargo 사용)
cargo install c2patool

# macOS (Homebrew 사용)
brew install c2patool

# Windows
# 다운로드: https://github.com/contentauth/c2patool/releases
```

#### 파일 검증

```bash
# 기본 검증
c2patool photo.jpg

# 상세한 JSON 출력
c2patool photo.jpg --detailed

# 매니페스트를 JSON 파일로 저장
c2patool photo.jpg --output manifest.json

# 여러 파일 확인
c2patool *.jpg
```

#### 예제 출력

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

### 방법 4: 프로그래밍 방식

**앱에 검증 통합:**

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

## C2PA 콘텐츠 생성

### 방법 1: 지원되는 소프트웨어 사용

**코딩 불필요:**

#### Adobe Photoshop/Lightroom

1. Photoshop/Lightroom에서 이미지 열기
2. **편집 → Content Credentials**로 이동
3. 크리에이터 정보 입력
4. 파일 저장 → C2PA 매니페스트가 자동으로 추가됨

#### C2PA 내장 카메라

- **Nikon Z9/Z8**: 카메라 설정에서 활성화 → 촬영 시 사진 서명
- **Leica M11-P/SL3**: 자동 서명 활성화됨
- **Sony Alpha 시리즈**: 펌웨어 업데이트를 통해 활성화

### 방법 2: 명령줄 (c2patool)

#### 필수 요소

서명 인증서가 필요합니다:

**테스트용(자체 서명):**
```bash
# 테스트 인증서 생성(검증자에게 신뢰받지 않음)
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes
```

**프로덕션용:**
- 신뢰할 수 있는 CA에서 인증서 구매(DigiCert, GlobalSign 등)
- C2PA 키 사용 요구 사항 지정

#### 매니페스트 생성

`manifest.json` 생성:

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

#### 파일 서명

```bash
# 인증서로 서명
c2patool photo.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed_photo.jpg

# 작동하는지 확인
c2patool signed_photo.jpg
```

### 방법 3: 프로그래밍 방식

#### Rust

```rust
use c2pa::{Builder, SigningAlg};

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let mut builder = Builder::from_file("input.jpg")?;

    // 크리에이터 어서션 추가
    builder.add_assertion("stds.schema-org.CreativeWork",
        r#"{"author": [{"name": "John Doe"}]}"#)?;

    // 서명 및 저장
    let signer = get_signer(); // 인증서/키
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

# 빌더 생성
builder = Builder.from_file('input.jpg')

# 어서션 추가
builder.add_assertion('stds.schema-org.CreativeWork', {
    'author': [{'name': 'John Doe'}]
})

# 서명
signer = Signer('cert.pem', 'key.pem')
builder.sign('output.jpg', signer)

print('Signed successfully!')
```

### 방법 4: 서명된 콘텐츠 편집 (출처 보존)

C2PA 서명 콘텐츠를 편집할 때 원본을 "재료"로 참조하세요:

```bash
# 편집하고 체인 보존
c2patool edited_photo.jpg \
  --parent original_photo.jpg \
  --manifest edit_manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output final_photo.jpg
```

새 매니페스트는 `original_photo.jpg`를 재료로 참조하여 전체 기록을 보존합니다.

---

## 다음 단계

### 더 알아보기

**규격 이해:**
- [English](../../docs/specifications/C2PA_Specification.pdf)
- [中文](../../docs/specifications/C2PA_Specification_zh-Hans.pdf)
- [日本語](../../docs/specifications/C2PA_Specification_ja.pdf)
- [Deutsch](../../docs/specifications/C2PA_Specification_de.pdf)

**도구 탐색:**
- [도구 및 라이브러리](README.md#도구-및-라이브러리) - 모든 주요 언어용 SDK
- [공식 문서](https://opensource.contentauthenticity.org/docs)

**일반적인 질문:**
- [FAQ](faq.md) - 25개 이상의 자주 묻는 질문
- [GitHub 토론](https://github.com/c2pa-org/../../docs/specifications/discussions)

### 튜토리얼 및 예제

**공식 튜토리얼:**
- [C2PA 개발자 튜토리얼](https://opensource.contentauthenticity.org/docs/tutorial)
- [매니페스트 생성](https://opensource.contentauthenticity.org/docs/manifest/guide)
- [어서션 참조](https://opensource.contentauthenticity.org/docs/manifest/assertions)

**코드 예제:**
- [c2pa-rs 예제](https://github.com/contentauth/c2pa-rs/tree/main/sdk/examples)
- [c2pa-node 예제](https://github.com/contentauth/c2pa-node/tree/main/examples)
- [c2pa-python 예제](https://github.com/contentauth/c2pa-python/tree/main/examples)

### 프로덕션 배포

**라이브로 전환하기 전에:**

1. **프로덕션 인증서 받기**
   - 신뢰할 수 있는 CA에서 구매(DigiCert, GlobalSign 등)
   - C2PA 호환 키 사용 확인
   - 비용: 연간 약 $50-500

2. **보안 키 저장소**
   - 개인 키에 대해 HSM(Hardware Security Module) 사용
   - 또는 클라우드 HSM(AWS CloudHSM, Azure Key Vault)
   - 소스 제어에 키를 커밋하지 마세요

3. **철저히 테스트**
   - 여러 검증자로 서명 확인
   - 다양한 파일 형식에서 테스트
   - 크로스 플랫폼 호환성 확인

4. **모니터링 및 유지 관리**
   - 인증서 교체 구현
   - 취소 모니터링
   - SDK를 최신 상태로 유지

### 애플리케이션과 통합

**주요 통합 지점:**

```
앱 워크플로:

1. 콘텐츠 생성/업로드
   ↓
2. [C2PA 매니페스트 추가] ← 통합 지점
   ↓
3. 인증서로 서명
   ↓
4. 서명된 콘텐츠 저장/게시
   ↓
5. [선택 사항] 표시 시 검증 ← 또 다른 통합 지점
```

**일반적인 통합 시간:**
- 간단한 검증: 1-2일
- 기본 서명: 3-5일
- 전체 프로덕션 배포: 2-4주

### 인증서 받기

**테스트(무료):**
- 자체 서명 인증서
- 개발에만 적합
- 검증자에게 신뢰받지 않음

**프로덕션:**
- **DigiCert**: https://www.digicert.com/
- **GlobalSign**: https://www.globalsign.com/
- **Entrust**: https://www.entrust.com/
- C2PA 키 사용 확장이 있는 인증서 요청

### 커뮤니티 참여

**도움 받기:**
- [GitHub 이슈](https://github.com/c2pa-org/../../docs/specifications/issues) - 버그 보고
- [GitHub 토론](https://github.com/c2pa-org/../../docs/specifications/discussions) - 질문
- [C2PA 웹사이트](https://c2pa.org) - 공식 리소스

**기여하기:**
- [awesome-c2pa](README.md) - 리소스 추가, 문서 번역
- [C2PA 구현](https://github.com/contentauth) - 코드 기여
- [Content Authenticity Initiative](https://contentauthenticity.org) - 운동에 참여

---

## 빠른 참조 카드

### 콘텐츠 검증
```bash
c2patool image.jpg
```

### 콘텐츠 서명
```bash
c2patool input.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed.jpg
```

### 웹에서 확인
```
https://contentcredentials.org/verify
```

### 일반적인 매니페스트 템플릿
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

## 문제 해결

### "No C2PA data found"
- 파일에 C2PA 매니페스트가 없을 수 있습니다
- 메타데이터가 제거되었을 수 있습니다
- 다른 파일 형식을 시도해 보세요

### "Invalid signature"
- 서명 후 파일이 수정되었습니다
- 인증서가 취소되었거나 만료되었습니다
- 신뢰 체인이 깨졌습니다

### "Certificate not trusted"
- 자체 서명 인증서 사용(테스트에서 예상됨)
- CA가 신뢰 목록에 없습니다
- 필요한 경우 사용자 정의 신뢰 앵커 추가

### 성능 문제
- C2PA는 매니페스트당 약 10-50KB를 추가합니다(최소)
- 서명은 일반적인 파일의 경우 1초 미만입니다
- 검증은 거의 즉시 이루어집니다

---

**시작할 준비가 되셨나요?** 위의 방법을 선택하고 시작하세요!

**질문이 있으신가요?** [FAQ](faq.md)를 확인하거나 [이슈를 열어주세요](https://github.com/paulortiz199928/awesome-c2pa/issues).

---

*최종 업데이트: 2025년 11월*
