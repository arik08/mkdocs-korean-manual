# 마이그레이션 가이드

## 📋 개요

이 가이드는 다른 문서 도구에서 MkDocs로 마이그레이션하는 방법을 설명합니다.

## 🔄 GitBook에서 MkDocs로

### 1. 구조 변환

**GitBook 구조:**
```
├── README.md
├── SUMMARY.md
├── chapter1/
│   ├── README.md
│   └── section1.md
└── chapter2/
    └── README.md
```

**MkDocs 구조:**
```
├── mkdocs.yml
├── docs/
│   ├── index.md (README.md에서)
│   ├── chapter1/
│   │   ├── index.md
│   │   └── section1.md
│   └── chapter2/
│       └── index.md
```

### 2. SUMMARY.md 변환

**GitBook SUMMARY.md:**
```markdown
# Summary

* [Introduction](README.md)
* [Chapter 1](chapter1/README.md)
  * [Section 1](chapter1/section1.md)
* [Chapter 2](chapter2/README.md)
```

**MkDocs mkdocs.yml:**
```yaml
nav:
  - 소개: index.md
  - Chapter 1:
    - 개요: chapter1/index.md
    - Section 1: chapter1/section1.md
  - Chapter 2: chapter2/index.md
```

### 3. 변환 스크립트 (Python)

```python
import os
import re
import shutil

def convert_gitbook_to_mkdocs(gitbook_path, mkdocs_path):
    # docs 디렉토리 생성
    docs_path = os.path.join(mkdocs_path, 'docs')
    os.makedirs(docs_path, exist_ok=True)
    
    # README.md를 index.md로 변환
    readme_path = os.path.join(gitbook_path, 'README.md')
    if os.path.exists(readme_path):
        shutil.copy2(readme_path, os.path.join(docs_path, 'index.md'))
    
    # 다른 파일들 복사
    for root, dirs, files in os.walk(gitbook_path):
        for file in files:
            if file.endswith('.md') and file != 'README.md' and file != 'SUMMARY.md':
                src_path = os.path.join(root, file)
                rel_path = os.path.relpath(src_path, gitbook_path)
                dest_path = os.path.join(docs_path, rel_path)
                
                os.makedirs(os.path.dirname(dest_path), exist_ok=True)
                shutil.copy2(src_path, dest_path)

# 사용법
convert_gitbook_to_mkdocs('/path/to/gitbook', '/path/to/mkdocs')
```

## 📖 Sphinx에서 MkDocs로

### 1. RST to Markdown 변환

**RST 파일:**
```rst
Installation
============

Quick Start
-----------

To install the package:

.. code-block:: bash

   pip install mypackage
```

**Markdown 변환:**
```markdown
# Installation

## Quick Start

To install the package:

```bash
pip install mypackage
```

### 2. 변환 도구

**Pandoc 사용:**
```bash
pandoc -f rst -t markdown input.rst -o output.md
```

**Python 스크립트:**
```python
import pypandoc

def convert_rst_to_md(rst_file, md_file):
    output = pypandoc.convert_file(rst_file, 'markdown', format='rst')
    with open(md_file, 'w', encoding='utf-8') as f:
        f.write(output)

# 사용법
convert_rst_to_md('index.rst', 'index.md')
```

### 3. conf.py를 mkdocs.yml로 변환

**Sphinx conf.py:**
```python
project = 'My Project'
author = 'Author Name'
html_theme = 'sphinx_rtd_theme'
extensions = ['sphinx.ext.autodoc']
```

**MkDocs mkdocs.yml:**
```yaml
site_name: My Project
site_author: Author Name
theme:
  name: material
plugins:
  - mkdocstrings
```

## 📚 Notion에서 MkDocs로

### 1. Notion 페이지 내보내기

1. Notion에서 페이지 선택
2. 우상단 "..." 메뉴 클릭
3. "Export" 선택
4. "Markdown & CSV" 선택
5. 파일 다운로드

### 2. 파일 정리

Notion 내보내기는 다음과 같은 구조를 생성합니다:

```
Export-abc123/
├── Page 1 abc123.md
├── Page 2 def456.md
└── images/
    ├── image1.png
    └── image2.png
```

정리된 구조로 변환:

```python
import os
import re
import shutil

def clean_notion_export(export_path, docs_path):
    os.makedirs(docs_path, exist_ok=True)
    images_path = os.path.join(docs_path, 'images')
    os.makedirs(images_path, exist_ok=True)
    
    for file in os.listdir(export_path):
        if file.endswith('.md'):
            # 파일명 정리 (해시 제거)
            clean_name = re.sub(r' [a-f0-9]{32}\.md$', '.md', file)
            clean_name = clean_name.replace(' ', '-').lower()
            
            src_path = os.path.join(export_path, file)
            dest_path = os.path.join(docs_path, clean_name)
            
            # 파일 내용의 이미지 경로 수정
            with open(src_path, 'r', encoding='utf-8') as f:
                content = f.read()
            
            # 이미지 경로 수정
            content = re.sub(r'!\[(.*?)\]\((.*?)\)', 
                           lambda m: f'![{m.group(1)}](images/{os.path.basename(m.group(2))})', 
                           content)
            
            with open(dest_path, 'w', encoding='utf-8') as f:
                f.write(content)
    
    # 이미지 파일 복사
    notion_images = os.path.join(export_path, 'images')
    if os.path.exists(notion_images):
        for img in os.listdir(notion_images):
            shutil.copy2(os.path.join(notion_images, img), 
                        os.path.join(images_path, img))
```

## 📝 WordPress에서 MkDocs로

### 1. WordPress 내보내기

1. WordPress 관리자 → 도구 → 내보내기
2. "모든 콘텐츠" 선택
3. XML 파일 다운로드

### 2. XML을 Markdown으로 변환

```python
import xml.etree.ElementTree as ET
import html2text
from datetime import datetime

def convert_wordpress_xml(xml_file, output_dir):
    tree = ET.parse(xml_file)
    root = tree.getroot()
    
    h = html2text.HTML2Text()
    h.ignore_links = False
    h.ignore_images = False
    
    for item in root.findall('.//item'):
        title = item.find('title').text
        content = item.find('{http://purl.org/rss/1.0/modules/content/}encoded').text
        
        if content and title:
            # HTML을 Markdown으로 변환
            markdown_content = h.handle(content)
            
            # 파일명 생성
            filename = title.replace(' ', '-').lower() + '.md'
            filename = re.sub(r'[^\w\-_\.]', '', filename)
            
            # 파일 저장
            with open(os.path.join(output_dir, filename), 'w', encoding='utf-8') as f:
                f.write(f'# {title}\n\n')
                f.write(markdown_content)
```

## 🛠️ 마이그레이션 체크리스트

### 변환 전 확인사항

- [ ] 기존 문서 백업
- [ ] 이미지 파일 위치 확인
- [ ] 내부 링크 패턴 파악
- [ ] 특별한 문법이나 플러그인 사용 여부

### 변환 과정

- [ ] 파일 구조 변환
- [ ] 콘텐츠 형식 변환
- [ ] 이미지 경로 수정
- [ ] 내부 링크 수정
- [ ] 네비게이션 구조 설정

### 변환 후 확인사항

- [ ] 모든 페이지가 정상 표시되는지 확인
- [ ] 이미지가 올바르게 로드되는지 확인
- [ ] 내부 링크가 작동하는지 확인
- [ ] 검색 기능 테스트
- [ ] 모바일에서 정상 표시 확인

## 🔄 자동화 스크립트

전체 마이그레이션을 자동화하는 스크립트:

```bash
#!/bin/bash

echo "=== MkDocs 마이그레이션 스크립트 ==="

# 디렉토리 생성
mkdir -p docs/images

# GitBook 변환 (예시)
if [ -f "SUMMARY.md" ]; then
    echo "GitBook 구조 감지됨"
    python convert_gitbook.py
fi

# Sphinx 변환 (예시)
if [ -f "conf.py" ]; then
    echo "Sphinx 구조 감지됨"
    python convert_sphinx.py
fi

# MkDocs 설정 생성
cat > mkdocs.yml << EOF
site_name: 마이그레이션된 사이트
site_description: 기존 문서를 MkDocs로 마이그레이션

theme:
  name: material
  language: ko

plugins:
  - search:
      lang: ko

nav:
  - 홈: index.md
EOF

echo "마이그레이션 완료!"
echo "다음 명령으로 미리보기하세요: mkdocs serve"
```

마이그레이션이 완료되면 `mkdocs serve`로 결과를 확인하세요!