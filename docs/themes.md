# 테마 가이드

## Material 테마 (권장)

Material 테마는 MkDocs에서 가장 인기 있는 테마입니다.

### 설치
```bash
pip install mkdocs-material
```

### 기본 설정
```yaml
theme:
  name: material
  language: ko
```

### 고급 설정
```yaml
theme:
  name: material
  language: ko
  features:
    - navigation.tabs
    - navigation.sections
    - navigation.expand
    - navigation.top
    - search.highlight
    - search.share
  palette:
    - scheme: default
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-7
        name: 다크 모드로 전환
    - scheme: slate
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-4
        name: 라이트 모드로 전환
```

## 색상 커스터마이징

### 사용 가능한 색상
- red, pink, purple, indigo
- blue, light blue, cyan, teal
- green, light green, lime
- yellow, amber, orange
- brown, grey, blue grey

### 커스텀 CSS
```yaml
extra_css:
  - assets/stylesheets/extra.css
```

```css
/* assets/stylesheets/extra.css */
:root {
  --md-primary-fg-color: #ff6b6b;
  --md-primary-fg-color--light: #ff8e8e;
}
```

## 다른 테마 옵션

### ReadTheDocs 테마
```yaml
theme:
  name: readthedocs
```

### 기본 테마
```yaml
theme:
  name: mkdocs
```

!!! tip "테마 선택 가이드"
    Material 테마를 권장합니다. 가장 많은 기능과 커스터마이징 옵션을 제공합니다.