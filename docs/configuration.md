# 기본 설정

## mkdocs.yml 파일 구조

MkDocs의 모든 설정은 `mkdocs.yml` 파일에서 관리됩니다.

```yaml
# 사이트 기본 정보
site_name: 사이트 이름
site_description: 사이트 설명
site_author: 작성자명
site_url: https://yourdomain.com

# 테마 설정
theme:
  name: material
  language: ko

# 네비게이션
nav:
  - 홈: index.md
  - 가이드: guide.md

# 플러그인
plugins:
  - search:
      lang: ko

# Markdown 확장
markdown_extensions:
  - admonition
  - pymdownx.highlight
  - pymdownx.superfences
```

## 네비게이션 설정

### 단순 구조
```yaml
nav:
  - 홈: index.md
  - 가이드: guide.md
  - API: api.md
```

### 계층 구조
```yaml
nav:
  - 홈: index.md
  - 시작하기:
    - 설치: getting-started/installation.md
    - 첫 프로젝트: getting-started/first-project.md
  - 가이드:
    - 기본 사용법: guide/basic.md
    - 고급 기능: guide/advanced.md
```

## Markdown 확장

### 기본 확장
```yaml
markdown_extensions:
  - admonition          # 경고/알림 박스
  - attr_list           # 속성 리스트
  - footnotes           # 각주
  - toc:                # 목차
      permalink: true
```

### PyMdown 확장
```yaml
markdown_extensions:
  - pymdownx.highlight:     # 코드 하이라이팅
      anchor_linenums: true
  - pymdownx.inlinehilite   # 인라인 코드
  - pymdownx.superfences    # 코드 블록 확장
  - pymdownx.tabbed:        # 탭
      alternate_style: true
```

## 추가 설정

### CSS/JS 파일 추가
```yaml
extra_css:
  - assets/stylesheets/extra.css

extra_javascript:
  - assets/javascripts/extra.js
```

### 소셜 링크
```yaml
extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/username
    - icon: fontawesome/brands/twitter
      link: https://twitter.com/username
```

!!! tip "설정 검증"
    `mkdocs config` 명령으로 현재 설정을 확인할 수 있습니다.