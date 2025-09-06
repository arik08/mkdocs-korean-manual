# 플러그인 가이드

## 필수 플러그인

### Search Plugin (내장)
```yaml
plugins:
  - search:
      lang: ko
```

### Git Revision Date
```bash
pip install mkdocs-git-revision-date-localized-plugin
```

```yaml
plugins:
  - git-revision-date-localized:
      type: date
      locale: ko
```

### Minify Plugin
```bash
pip install mkdocs-minify-plugin
```

```yaml
plugins:
  - minify:
      minify_html: true
      minify_js: true
      minify_css: true
```

## 유용한 플러그인

### Tags Plugin
```yaml
plugins:
  - tags:
      tags_file: tags.md
```

### MkDocstrings (API 문서 자동 생성)
```bash
pip install mkdocstrings[python]
```

```yaml
plugins:
  - mkdocstrings:
      default_handler: python
```

사용법:
```markdown
::: my_module.my_function
```

### PDF Export
```bash
pip install mkdocs-pdf-export-plugin
```

```yaml
plugins:
  - pdf-export:
      verbose: true
      combined: true
```

## 플러그인 설정 예시

완전한 플러그인 설정:

```yaml
plugins:
  - search:
      lang: ko
  - git-revision-date-localized:
      type: date
      locale: ko
  - minify:
      minify_html: true
  - tags:
      tags_file: tags.md
```

!!! warning "플러그인 충돌"
    일부 플러그인은 서로 충돌할 수 있습니다. 문제가 발생하면 하나씩 비활성화해보세요.

!!! tip "플러그인 찾기"
    더 많은 플러그인은 [PyPI](https://pypi.org/search/?q=mkdocs)에서 찾을 수 있습니다.