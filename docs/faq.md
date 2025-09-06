# 자주 묻는 질문 (FAQ)

## 🚀 시작하기

### Q: MkDocs를 왜 사용해야 하나요?
**A:** MkDocs는 다음과 같은 장점이 있습니다:
- **간단함**: Markdown으로 쉽게 문서 작성
- **빠름**: 정적 사이트로 빠른 로딩
- **예쁨**: Material 테마로 모던한 디자인
- **검색**: 강력한 내장 검색 기능
- **무료**: GitHub Pages 등에 무료 호스팅

### Q: 프로그래밍 지식이 없어도 사용할 수 있나요?
**A:** 네! MkDocs는 비개발자도 쉽게 사용할 수 있습니다:
- Markdown 문법만 알면 됨
- 설정은 간단한 YAML 파일
- 웹 브라우저에서 실시간 미리보기

## 📝 콘텐츠 작성

### Q: Markdown을 처음 접하는데 어떻게 배우나요?
**A:** Markdown은 매우 간단합니다:

```markdown
# 제목 1
## 제목 2

**굵은 글씨**
*기울임*

- 목록 항목 1
- 목록 항목 2

[링크 텍스트](URL)
![이미지](이미지경로)
```

### Q: 이미지는 어디에 저장해야 하나요?
**A:** `docs/` 폴더 내에 이미지 폴더를 만드세요:

```
docs/
├── images/
│   ├── screenshot1.png
│   └── diagram.svg
├── index.md
└── guide.md
```

사용법:
```markdown
![스크린샷](images/screenshot1.png)
```

### Q: 동영상을 삽입할 수 있나요?
**A:** HTML을 사용하여 동영상을 삽입할 수 있습니다:

```html
<video width="100%" controls>
  <source src="videos/demo.mp4" type="video/mp4">
</video>
```

## 🎨 디자인과 테마

### Q: 로고를 추가하려면 어떻게 하나요?
**A:** 테마 설정에서 추가할 수 있습니다:

```yaml
theme:
  name: material
  logo: assets/images/logo.png
  favicon: assets/images/favicon.ico
```

### Q: 사이트 색상을 변경하고 싶어요
**A:** Material 테마에서 색상 변경:

```yaml
theme:
  name: material
  palette:
    primary: blue
    accent: light blue
```

### Q: 다크 모드를 지원하나요?
**A:** 네, Material 테마에서 지원합니다:

```yaml
theme:
  name: material
  palette:
    - scheme: default
      toggle:
        icon: material/brightness-7
        name: 다크 모드로 전환
    - scheme: slate
      toggle:
        icon: material/brightness-4
        name: 라이트 모드로 전환
```

## 🔧 설정과 기능

### Q: 검색이 한글을 지원하지 않아요
**A:** 검색 플러그인에서 언어를 설정하세요:

```yaml
plugins:
  - search:
      lang: ko
```

### Q: 사이드바 메뉴 순서를 바꾸고 싶어요
**A:** `nav` 섹션에서 순서를 조정하세요:

```yaml
nav:
  - 홈: index.md
  - 먼저 보여줄 페이지: first.md
  - 나중에 보여줄 페이지: second.md
```

## 🚀 배포와 호스팅

### Q: 무료로 호스팅할 수 있는 곳이 있나요?
**A:** 여러 무료 옵션이 있습니다:

1. **GitHub Pages** (권장)
   - 가장 인기 있는 선택
   - GitHub Actions로 자동 배포

2. **Netlify**
   - 간단한 드래그 앤 드롭 배포
   - CDN 제공

3. **Vercel**
   - 매우 빠른 배포
   - 자동 HTTPS

### Q: GitHub Pages 배포가 실패해요
**A:** 흔한 원인들:

1. **site_url 설정**
   ```yaml
   site_url: https://username.github.io/repository-name/
   ```

2. **권한 확인**
   - Settings → Actions → General → Workflow permissions
   - "Read and write permissions" 선택

## 💡 팁과 모범 사례

### Q: 문서 작성 시 주의할 점이 있나요?
**A:** 다음 모범 사례를 따르세요:

1. **일관된 구조**
   ```
   # 제목 (H1은 페이지당 하나)
   ## 주요 섹션
   ### 하위 섹션
   ```

2. **명확한 파일명**
   ```
   installation.md      (O)
   how-to-install.md    (O)
   설치방법.md          (X)
   ```

### Q: SEO를 개선하려면?
**A:** 다음 설정들을 추가하세요:

```yaml
site_description: 상세한 사이트 설명
site_url: https://yourdomain.com

plugins:
  - sitemap
```

이 FAQ가 도움이 되었나요? 더 궁금한 점이 있다면 언제든 문의하세요!