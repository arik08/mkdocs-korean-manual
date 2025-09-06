# 완전한 설정 가이드

## 📋 mkdocs.yml 완전 가이드

다음은 모든 주요 기능을 포함한 완전한 `mkdocs.yml` 설정 예제입니다.

```yaml
# ==============================================================================
# 기본 사이트 정보
# ==============================================================================
site_name: 완전한 MkDocs 가이드
site_description: MkDocs를 활용한 완벽한 문서 사이트 구축 가이드
site_author: 개발자 이름
site_url: https://username.github.io/repository-name/

# 저장소 정보 (GitHub 연동)
repo_name: username/repository-name
repo_url: https://github.com/username/repository-name
edit_uri: edit/main/docs/

# 저작권 정보
copyright: |
  &copy; 2024 <a href="https://github.com/username" target="_blank" rel="noopener">개발자 이름</a>

# ==============================================================================
# 테마 설정 (Material Theme)
# ==============================================================================
theme:
  name: material
  language: ko
  
  # 커스텀 디렉토리
  custom_dir: overrides
  
  # 색상 팔레트
  palette:
    # 라이트 모드
    - media: "(prefers-color-scheme: light)"
      scheme: default
      primary: blue
      accent: light blue
      toggle:
        icon: material/brightness-7
        name: 다크 모드로 전환
    
    # 다크 모드
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      primary: blue
      accent: light blue
      toggle:
        icon: material/brightness-4
        name: 라이트 모드로 전환
  
  # 폰트 설정
  font:
    text: Noto Sans KR
    code: Roboto Mono
  
  # 파비콘 및 로고
  favicon: assets/images/favicon.png
  logo: assets/images/logo.svg
  
  # 기능 활성화
  features:
    # 네비게이션
    - navigation.instant        # 즉시 로딩
    - navigation.instant.prefetch  # 프리페치
    - navigation.instant.progress  # 진행 표시
    - navigation.tracking       # URL 추적
    - navigation.tabs           # 상단 탭
    - navigation.tabs.sticky    # 고정 탭
    - navigation.sections       # 섹션 표시
    - navigation.expand         # 섹션 확장
    - navigation.path           # 경로 표시
    - navigation.prune          # 불필요한 항목 제거
    - navigation.indexes        # 인덱스 페이지
    - navigation.top            # 맨 위로 버튼
    - navigation.footer         # 하단 네비게이션
    
    # 목차 (TOC)
    - toc.follow               # 목차 따라가기
    - toc.integrate            # 목차 통합
    
    # 검색
    - search.highlight         # 검색 결과 하이라이트
    - search.share             # 검색 공유
    - search.suggest           # 검색 제안
    
    # 헤더
    - header.autohide          # 헤더 자동 숨김
    
    # 콘텐츠
    - content.action.edit      # 편집 버튼
    - content.action.view      # 소스 보기 버튼
    - content.code.annotate    # 코드 주석
    - content.code.copy        # 코드 복사
    - content.code.select      # 코드 선택
    - content.tabs.link        # 탭 링크
    - content.tooltips         # 툴팁

# ==============================================================================
# 플러그인 설정
# ==============================================================================
plugins:
  # 검색 플러그인
  - search:
      lang: 
        - ko
        - en
      separator: '[\s\-,:!=\[\]()"/]+|(?!\b)(?=[A-Z][a-z])|\.(?!\d)|&[lg]t;'
      prebuild_index: true
  
  # Git 정보 플러그인
  - git-revision-date-localized:
      type: datetime
      locale: ko
      timezone: Asia/Seoul
      enable_creation_date: true
      exclude:
        - index.md
        - tags.md
  
  # Git 작성자 정보
  - git-authors:
      show_contribution: true
      show_line_count: true
      count_empty_lines: false
      exclude:
        - index.md
  
  # 코드 최적화
  - minify:
      minify_html: true
      minify_css: true
      minify_js: true
      htmlmin_opts:
        remove_comments: true
        remove_empty_space: true
      cache_safe: true
  
  # 태그 시스템
  - tags:
      tags_file: tags.md
  
  # 소셜 카드 생성
  - social:
      cards: true
      cards_layout_options:
        background_color: "#2196F3"
        color: "#FFFFFF"
        font_family: Noto Sans KR
  
  # 블로그 기능
  - blog:
      blog_dir: blog
      blog_toc: true
      post_date_format: full
      post_url_format: "{date}/{slug}"
      post_excerpt: required
      pagination_per_page: 5
      authors_file: "{blog}/.authors.yml"
  
  # 사이트맵 생성
  - sitemap:
      canonical_url: https://username.github.io/repository-name/
      use_directory_urls: true
  
  # 오프라인 검색
  - offline:
      enabled: !ENV [OFFLINE, false]
  
  # 이미지 최적화
  - optimize:
      enabled: !ENV [CI, false]
      cache: true
      cache_dir: .cache/plugins/optimize
      optimize_png: true
      optimize_jpg: true
      optimize_svg: true
  
  # i18n 다국어 지원
  - i18n:
      docs_structure: folder
      fallback_to_default: true
      reconfigure_material: true
      reconfigure_search: true
      languages:
        - locale: ko
          default: true
          name: 한국어
          build: true
        - locale: en
          name: English
          build: true
          nav_translations:
            시작하기: Getting Started
            가이드: Guide
            API 문서: API Documentation
            참조: Reference

# ==============================================================================
# Markdown 확장
# ==============================================================================
markdown_extensions:
  # Python Markdown 기본 확장
  - abbr
  - admonition
  - attr_list
  - def_list
  - footnotes
  - md_in_html
  - meta
  - tables
  - toc:
      permalink: true
      toc_depth: 3
  
  # PyMdown Extensions
  - pymdownx.arithmatex:
      generic: true
  - pymdownx.betterem:
      smart_enable: all
  - pymdownx.caret
  - pymdownx.details
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
      linenums: true
      use_pygments: true
      pygments_style: github
  - pymdownx.inlinehilite
  - pymdownx.keys
  - pymdownx.magiclink:
      normalize_issue_symbols: true
      repo_url_shorthand: true
      user: username
      repo: repository-name
  - pymdownx.mark
  - pymdownx.smartsymbols
  - pymdownx.snippets:
      base_path: 
        - docs
        - includes
      check_paths: true
      restrict_base_path: true
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
  - pymdownx.tabbed:
      alternate_style: true
      combine_header_slug: true
      slugify: !!python/object/apply:pymdownx.slugs.slugify
        kwds:
          case: lower
  - pymdownx.tasklist:
      custom_checkbox: true
  - pymdownx.tilde
  - pymdownx.critic:
      mode: view
  - pymdownx.blocks.admonition:
      types:
        - note
        - abstract
        - info
        - tip
        - success
        - question
        - warning
        - failure
        - danger
        - bug
        - example
        - quote

# ==============================================================================
# 네비게이션 구조
# ==============================================================================
nav:
  - 홈: index.md
  
  - 시작하기:
    - 소개: getting-started.md
    - 설치: installation.md
    - 첫 번째 프로젝트: first-project.md
  
  - 가이드:
    - 기본 사용법: guide.md
    - 설정: configuration.md
    - 플러그인: plugins.md
    - 테마: themes.md
    - 배포: deployment.md
    - 고급 기능: advanced-features.md
    - 완전한 설정: complete-configuration.md
  
  - 참조:
    - API 문서: api.md
    - CLI 명령어: cli-reference.md
    - 클래스 및 메서드: classes.md
  
  - 도움말:
    - 문제 해결: troubleshooting.md
    - FAQ: faq.md
    - 마이그레이션: migration.md
    - 모범 사례: best-practices.md
  
  - 블로그: 
    - blog/index.md
  
  - 태그: tags.md

# ==============================================================================
# 추가 리소스
# ==============================================================================
extra_css:
  - stylesheets/extra.css
  - stylesheets/custom.css
  - https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&display=swap

extra_javascript:
  - javascripts/extra.js
  - javascripts/mathjax.js
  - https://polyfill.io/v3/polyfill.min.js?features=es6
  - https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js
  - https://unpkg.com/mermaid@8.14.0/dist/mermaid.min.js

# ==============================================================================
# 추가 설정
# ==============================================================================
extra:
  # 소셜 링크
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/username
      name: GitHub
    - icon: fontawesome/brands/twitter
      link: https://twitter.com/username
      name: Twitter
    - icon: fontawesome/brands/linkedin
      link: https://linkedin.com/in/username
      name: LinkedIn
    - icon: fontawesome/solid/envelope
      link: mailto:email@example.com
      name: Email
  
  # 분석 도구
  analytics:
    provider: google
    property: G-XXXXXXXXXX
    feedback:
      title: 이 페이지가 도움이 되었나요?
      ratings:
        - icon: material/emoticon-happy-outline
          name: 좋음
          data: good
          note: >-
            좋은 피드백 감사합니다! 
            <a href="https://github.com/username/repository-name/issues" target="_blank" rel="noopener">GitHub</a>에서
            더 많은 정보를 찾을 수 있습니다.
        - icon: material/emoticon-sad-outline
          name: 개선이 필요함
          data: bad
          note: >- 
            피드백을 남겨주세요. 
            <a href="https://github.com/username/repository-name/issues/new" target="_blank" rel="noopener">
            이슈를 생성</a>하여 개선점을 알려주세요.
  
  # 버전 정보
  version:
    provider: mike
    default: stable
    alias: true
  
  # 동의 설정 (GDPR)
  consent:
    title: 쿠키 동의
    description: >- 
      당사는 귀하의 웹사이트 경험을 개인화하고 개선하기 위해 쿠키를 사용합니다.
      계속 진행하면 쿠키 정책에 동의하는 것입니다.
    actions:
      - accept
      - manage
      - reject
    cookies:
      analytics:
        name: Google Analytics
        checked: false
      github:
        name: GitHub
        checked: true

# ==============================================================================
# 개발 서버 설정
# ==============================================================================
dev_addr: '127.0.0.1:8000'
use_directory_urls: true
strict: true

# ==============================================================================
# 빌드 설정
# ==============================================================================
site_dir: site
docs_dir: docs

# 제외할 파일/디렉토리
exclude_docs: |
  drafts/
  private/
  *.tmp
  *.bak

# Hooks (사용자 정의 스크립트)
hooks:
  - hooks/on_config.py
  - hooks/on_pre_build.py
  - hooks/on_post_build.py

# ==============================================================================
# 환경별 설정
# ==============================================================================
# 환경변수 사용 예시:
# site_url: !ENV [SITE_URL, 'http://localhost:8000']
# 빌드 시: SITE_URL=https://mydomain.com mkdocs build
```

## 🎨 커스텀 CSS 예제

**stylesheets/extra.css:**
```css
/* ==============================================================================
   커스텀 변수
   ============================================================================== */
:root {
  --md-primary-fg-color: #2196F3;
  --md-primary-fg-color--light: #64B5F6;
  --md-primary-fg-color--dark: #1976D2;
  --md-accent-fg-color: #03DAC6;
  
  /* 한국 웹폰트 최적화 */
  --md-text-font: "Noto Sans KR", -apple-system, BlinkMacSystemFont, Helvetica, Arial, sans-serif;
  --md-code-font: "Roboto Mono", SFMono-Regular, Consolas, Menlo, monospace;
}

/* ==============================================================================
   타이포그래피
   ============================================================================== */
.md-typeset {
  font-size: 0.8rem;
  line-height: 1.7;
  color: var(--md-default-fg-color);
}

.md-typeset h1 {
  color: var(--md-primary-fg-color);
  font-weight: 700;
}

.md-typeset h2 {
  border-bottom: 2px solid var(--md-primary-fg-color--light);
  padding-bottom: 0.3rem;
}

/* ==============================================================================
   코드 블록 개선
   ============================================================================== */
.md-typeset .highlight {
  border-left: 4px solid var(--md-primary-fg-color);
  border-radius: 0.2rem;
  margin: 1em 0;
}

.md-typeset .highlight pre {
  margin: 0;
  padding: 1rem;
  background-color: var(--md-code-bg-color);
  border-radius: 0 0.2rem 0.2rem 0;
}

.md-typeset code {
  background-color: var(--md-code-bg-color);
  border-radius: 0.2rem;
  padding: 0.1em 0.3em;
  font-size: 0.85em;
}

/* ==============================================================================
   버튼 스타일
   ============================================================================== */
.md-button {
  background-color: var(--md-primary-fg-color);
  border: none;
  border-radius: 0.3rem;
  color: white;
  padding: 0.6rem 1.2rem;
  text-decoration: none;
  display: inline-block;
  transition: all 0.2s;
  font-weight: 500;
}

.md-button:hover {
  background-color: var(--md-primary-fg-color--dark);
  transform: translateY(-1px);
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
}

.md-button--secondary {
  background-color: transparent;
  border: 2px solid var(--md-primary-fg-color);
  color: var(--md-primary-fg-color);
}

.md-button--secondary:hover {
  background-color: var(--md-primary-fg-color);
  color: white;
}

/* ==============================================================================
   카드 스타일
   ============================================================================== */
.md-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
  margin: 1rem 0;
}

.md-card {
  background: var(--md-default-bg-color);
  border-radius: 0.5rem;
  padding: 1.5rem;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: all 0.3s;
  border-left: 4px solid var(--md-primary-fg-color);
}

.md-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 16px rgba(0,0,0,0.15);
}

.md-card__title {
  color: var(--md-primary-fg-color);
  font-weight: 600;
  margin-bottom: 0.5rem;
}

/* ==============================================================================
   네비게이션 개선
   ============================================================================== */
.md-nav__item--active .md-nav__link {
  color: var(--md-primary-fg-color);
  font-weight: 600;
}

.md-nav__link:hover {
  color: var(--md-primary-fg-color--light);
}

/* ==============================================================================
   반응형 개선
   ============================================================================== */
@media (max-width: 768px) {
  .md-typeset {
    font-size: 0.7rem;
  }
  
  .md-grid {
    grid-template-columns: 1fr;
  }
  
  .md-button {
    display: block;
    text-align: center;
    margin: 0.5rem 0;
  }
}

/* ==============================================================================
   다크 모드 최적화
   ============================================================================== */
[data-md-color-scheme="slate"] {
  --md-primary-fg-color: #64B5F6;
  --md-primary-fg-color--light: #90CAF9;
  --md-primary-fg-color--dark: #42A5F5;
}

[data-md-color-scheme="slate"] .md-card {
  background: var(--md-default-bg-color);
  border-left-color: var(--md-primary-fg-color--light);
}

/* ==============================================================================
   프린트 최적화
   ============================================================================== */
@media print {
  .md-header,
  .md-tabs,
  .md-sidebar,
  .md-footer {
    display: none !important;
  }
  
  .md-main__inner {
    margin: 0 !important;
  }
  
  .md-content {
    max-width: none !important;
  }
}

/* ==============================================================================
   애니메이션
   ============================================================================== */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

.md-typeset .admonition {
  animation: fadeIn 0.5s ease-out;
}

/* ==============================================================================
   접근성 개선
   ============================================================================== */
.md-skip {
  position: absolute;
  top: -40px;
  left: 6px;
  z-index: 1000;
  background: var(--md-primary-fg-color);
  color: white;
  padding: 8px;
  border-radius: 0.3rem;
  text-decoration: none;
}

.md-skip:focus {
  top: 6px;
}

/* 고대비 모드 지원 */
@media (prefers-contrast: high) {
  :root {
    --md-primary-fg-color: #000080;
    --md-default-fg-color: #000000;
    --md-default-bg-color: #ffffff;
  }
}

/* 애니메이션 감소 모드 */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

이 완전한 설정을 사용하면 프로페셔널하고 기능이 풍부한 MkDocs 사이트를 만들 수 있습니다! 🎉