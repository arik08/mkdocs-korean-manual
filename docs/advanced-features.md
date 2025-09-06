# 고급 기능 및 활용법

## 🎨 Material 테마 고급 커스터마이징

### 1. 커스텀 CSS 추가

**디렉토리 구조:**
```
docs/
├── stylesheets/
│   └── extra.css
└── index.md
```

**mkdocs.yml 설정:**
```yaml
theme:
  name: material
extra_css:
  - stylesheets/extra.css
```

**extra.css 예시:**
```css
/* 브랜드 컬러 적용 */
:root {
  --md-primary-fg-color: #2196F3;
  --md-primary-fg-color--light: #42A5F5;
  --md-primary-fg-color--dark: #1976D2;
}

/* 커스텀 버튼 스타일 */
.md-button--custom {
  background-color: var(--md-primary-fg-color);
  border-radius: 20px;
  padding: 10px 20px;
}

/* 코드 블록 커스터마이징 */
.highlight pre {
  border-left: 4px solid var(--md-primary-fg-color);
}
```

### 2. 커스텀 JavaScript

**js/custom.js:**
```javascript
// 페이지 로드 시 실행
document.addEventListener('DOMContentLoaded', function() {
  // 외부 링크에 아이콘 추가
  var links = document.querySelectorAll('a[href^="http"]');
  links.forEach(function(link) {
    if (!link.hostname.includes(window.location.hostname)) {
      link.innerHTML += ' <i class="fas fa-external-link-alt"></i>';
      link.setAttribute('target', '_blank');
      link.setAttribute('rel', 'noopener noreferrer');
    }
  });
  
  // 코드 복사 버튼 개선
  document.querySelectorAll('pre code').forEach(function(block) {
    var button = document.createElement('button');
    button.className = 'copy-code-btn';
    button.textContent = '복사';
    button.addEventListener('click', function() {
      navigator.clipboard.writeText(block.textContent);
      button.textContent = '복사됨!';
      setTimeout(() => button.textContent = '복사', 2000);
    });
    block.parentNode.appendChild(button);
  });
});
```

**mkdocs.yml에 추가:**
```yaml
extra_javascript:
  - js/custom.js
  - https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/js/all.min.js
```

### 3. 커스텀 템플릿

**overrides/main.html:**
```html
{% extends "base.html" %}

{% block announce %}
  <div class="md-banner">
    <div class="md-banner__inner md-grid md-typeset">
      📢 새로운 버전 v2.0이 출시되었습니다! 
      <a href="/changelog/">변경사항 보기</a>
    </div>
  </div>
{% endblock %}

{% block footer %}
  {{ super() }}
  <div class="md-footer-custom">
    <div class="md-grid md-typeset">
      <p>© 2024 My Company. 모든 권리 보유.</p>
    </div>
  </div>
{% endblock %}
```

## 🔌 고급 플러그인 활용

### 1. mkdocs-material 확장

```bash
pip install mkdocs-material[imaging]
```

```yaml
plugins:
  - optimize:
      enabled: !ENV [CI, false]
  - social:
      cards_layout_options:
        background_color: "#2196F3"
        color: "#FFFFFF"
```

### 2. 태그 시스템 구축

```yaml
plugins:
  - tags:
      tags_file: tags.md

theme:
  features:
    - content.tabs.link
    - content.code.annotate
```

**문서에 태그 추가:**
```markdown
---
tags:
  - Python
  - API
  - 고급
---

# API 고급 가이드
```

### 3. 블로그 기능 추가

```bash
pip install mkdocs-material mkdocs-blog-plugin
```

```yaml
plugins:
  - blog:
      blog_dir: blog
      post_date_format: medium
      post_url_format: "{date}/{slug}"
```

## 📊 SEO 및 성능 최적화

### 1. 구조화된 데이터 추가

**메타 데이터 설정:**
```yaml
# mkdocs.yml
site_name: 나의 기술 블로그
site_description: 개발 관련 팁과 가이드를 제공하는 블로그
site_author: 개발자 이름
site_url: https://myblog.github.io

extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/myusername
    - icon: fontawesome/brands/twitter
      link: https://twitter.com/myhandle
```

**페이지별 메타데이터:**
```markdown
---
title: Python 웹 크롤링 완벽 가이드
description: BeautifulSoup과 Selenium을 사용한 웹 크롤링 방법
keywords: python, 웹크롤링, beautifulsoup, selenium
author: 개발자 이름
date: 2024-01-15
---
```

### 2. 사이트맵 및 RSS 생성

```yaml
plugins:
  - sitemap:
      canonical_url: https://myblog.github.io/
  - rss:
      match_path: blog/posts/.*
      date_from_meta:
        as_creation: date
```

### 3. 이미지 최적화

```yaml
plugins:
  - optimize:
      cache: true
      cache_dir: .cache/plugins/optimize
      optimize_png: true
      optimize_jpg: true
      optimize_svg: true
```

## 🌍 다국어 지원

### 1. 언어별 사이트 구조

```
docs/
├── en/
│   ├── index.md
│   └── guide.md
├── ko/
│   ├── index.md
│   └── guide.md
└── index.md
```

### 2. 다국어 설정

```yaml
plugins:
  - i18n:
      docs_structure: folder
      languages:
        - locale: en
          default: true
          name: English
          build: true
        - locale: ko
          name: 한국어
          build: true
          nav_translations:
            Home: 홈
            Guide: 가이드
```

### 3. 언어 전환 버튼

```html
<!-- overrides/partials/header.html -->
<div class="md-header__option">
  <div class="md-select">
    <button class="md-select__inner" aria-label="언어 선택">
      <span class="md-select__current">{{ config.theme.language | default('en') }}</span>
    </button>
    <ul class="md-select__list">
      <li class="md-select__item">
        <a href="/en/" class="md-select__link">English</a>
      </li>
      <li class="md-select__item">
        <a href="/ko/" class="md-select__link">한국어</a>
      </li>
    </ul>
  </div>
</div>
```

## 🔍 고급 검색 기능

### 1. 검색 설정 최적화

```yaml
plugins:
  - search:
      separator: '[\s\-,:!=\[\]()"/]+|(?!\b)(?=[A-Z][a-z])|\.(?!\d)|&[lg]t;'
      lang: 
        - ko
        - en
      prebuild_index: python
```

### 2. 커스텀 검색 스크립트

```python
# scripts/build_search_index.py
import json
import os
from pathlib import Path

def build_custom_search_index():
    docs_dir = Path("docs")
    search_index = []
    
    for md_file in docs_dir.rglob("*.md"):
        with open(md_file, 'r', encoding='utf-8') as f:
            content = f.read()
            
        # 메타데이터 추출
        if content.startswith('---'):
            parts = content.split('---', 2)
            if len(parts) >= 3:
                metadata = parts[1]
                content = parts[2]
        
        # 검색 인덱스에 추가
        search_index.append({
            'title': extract_title(content),
            'url': str(md_file.relative_to(docs_dir)),
            'content': content[:500],  # 처음 500자만
            'keywords': extract_keywords(content)
        })
    
    with open('docs/search_index.json', 'w', encoding='utf-8') as f:
        json.dump(search_index, f, ensure_ascii=False, indent=2)

def extract_title(content):
    lines = content.split('\n')
    for line in lines:
        if line.startswith('# '):
            return line[2:].strip()
    return "제목 없음"

def extract_keywords(content):
    # 간단한 키워드 추출 로직
    import re
    words = re.findall(r'\b\w+\b', content.lower())
    return list(set(words))[:10]  # 상위 10개 키워드

if __name__ == "__main__":
    build_custom_search_index()
```

## 🚀 자동화 및 CI/CD

### 1. GitHub Actions 고급 설정

```yaml
# .github/workflows/ci.yml
name: CI/CD Pipeline
on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.11'
    
    - name: Install dependencies
      run: |
        pip install -r requirements.txt
        pip install pytest pytest-cov
    
    - name: Run tests
      run: |
        pytest tests/ --cov=./ --cov-report=xml
    
    - name: Build docs
      run: mkdocs build --strict
    
    - name: Test links
      run: |
        pip install pytest-html-report
        python scripts/test_links.py

  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
    - uses: actions/checkout@v4
      with:
        fetch-depth: 0
    
    - name: Setup Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.11'
    
    - name: Install dependencies
      run: |
        pip install -r requirements.txt
    
    - name: Deploy to GitHub Pages
      run: |
        git config --global user.name "GitHub Actions"
        git config --global user.email "actions@github.com"
        mkdocs gh-deploy --force
```

### 2. 자동 콘텐츠 업데이트

```python
# scripts/update_changelog.py
import os
import re
from datetime import datetime
import subprocess

def update_changelog():
    # Git 로그에서 변경사항 추출
    result = subprocess.run(
        ['git', 'log', '--oneline', '--since="1 month ago"'],
        capture_output=True, text=True
    )
    
    commits = result.stdout.strip().split('\n')
    
    # CHANGELOG.md 업데이트
    changelog_content = f"""# 변경사항

## {datetime.now().strftime('%Y-%m-%d')}

### 새로운 기능
"""
    
    for commit in commits:
        if 'feat:' in commit:
            changelog_content += f"- {commit.split('feat:')[1].strip()}\n"
    
    changelog_content += "\n### 버그 수정\n"
    for commit in commits:
        if 'fix:' in commit:
            changelog_content += f"- {commit.split('fix:')[1].strip()}\n"
    
    with open('docs/changelog.md', 'w', encoding='utf-8') as f:
        f.write(changelog_content)

if __name__ == "__main__":
    update_changelog()
```

## 🎯 성능 모니터링

### 1. 빌드 시간 최적화

```yaml
# mkdocs.yml
plugins:
  - search:
      prebuild_index: true  # 인덱스 사전 빌드
  - minify:
      minify_html: true
      minify_css: true
      minify_js: true
      cache_safe: true
```

### 2. 분석 도구 통합

```html
<!-- overrides/main.html -->
{% block scripts %}
  {{ super() }}
  
  <!-- Google Analytics -->
  <script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
  <script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', 'GA_MEASUREMENT_ID');
  </script>
  
  <!-- 사용자 정의 분석 -->
  <script>
    // 페이지 조회수 추적
    document.addEventListener('DOMContentLoaded', function() {
      // 스크롤 깊이 측정
      let maxScroll = 0;
      window.addEventListener('scroll', function() {
        const scrollPercent = (window.scrollY / (document.body.scrollHeight - window.innerHeight)) * 100;
        maxScroll = Math.max(maxScroll, scrollPercent);
      });
      
      // 페이지 떠날 때 데이터 전송
      window.addEventListener('beforeunload', function() {
        gtag('event', 'scroll_depth', {
          'custom_parameter': Math.round(maxScroll)
        });
      });
    });
  </script>
{% endblock %}
```

이러한 고급 기능들을 활용하면 더욱 전문적이고 강력한 문서 사이트를 만들 수 있습니다! 🚀