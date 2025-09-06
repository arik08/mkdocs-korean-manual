# 클래스 및 메서드 참조

## 📋 개요

MkDocs는 Python으로 작성되어 있으며, 확장이나 커스터마이징을 위해 다양한 클래스와 메서드를 제공합니다. 이 문서는 주요 API를 설명합니다.

## 🏗️ 핵심 클래스

### Config 클래스

MkDocs 설정을 관리하는 핵심 클래스입니다.

```python
from mkdocs.config import Config

class Config:
    """MkDocs 설정 관리 클래스"""
    
    def __init__(self, schema):
        """
        설정 초기화
        
        Args:
            schema: 설정 스키마
        """
        pass
    
    def load_file(self, config_file):
        """
        설정 파일 로드
        
        Args:
            config_file (str): 설정 파일 경로
            
        Returns:
            dict: 로드된 설정
        """
        pass
    
    def validate(self):
        """
        설정 검증
        
        Returns:
            tuple: (errors, warnings)
        """
        pass
```

**사용 예제:**
```python
from mkdocs.config import load_config

# 설정 파일 로드
config = load_config('mkdocs.yml')

# 설정 값 접근
site_name = config['site_name']
theme = config['theme']
plugins = config['plugins']
```

### Theme 클래스

테마 관련 기능을 제공합니다.

```python
from mkdocs.theme import Theme

class Theme:
    """테마 관리 클래스"""
    
    def __init__(self, name, custom_dir=None):
        """
        테마 초기화
        
        Args:
            name (str): 테마 이름
            custom_dir (str): 커스텀 디렉토리
        """
        self.name = name
        self.custom_dir = custom_dir
    
    @property
    def dirs(self):
        """
        테마 디렉토리 목록 반환
        
        Returns:
            list: 디렉토리 경로 목록
        """
        pass
    
    def get_env(self):
        """
        Jinja2 환경 반환
        
        Returns:
            jinja2.Environment: Jinja2 환경
        """
        pass
```

**사용 예제:**
```python
from mkdocs.theme import Theme

# 테마 인스턴스 생성
theme = Theme('material')

# 테마 디렉토리 확인
print(theme.dirs)

# Jinja2 환경 가져오기
env = theme.get_env()
```

### File 클래스

문서 파일을 나타냅니다.

```python
from mkdocs.structure.files import File

class File:
    """문서 파일 클래스"""
    
    def __init__(self, path, src_dir, dest_dir, use_directory_urls):
        """
        파일 초기화
        
        Args:
            path (str): 파일 경로
            src_dir (str): 소스 디렉토리
            dest_dir (str): 대상 디렉토리
            use_directory_urls (bool): 디렉토리 URL 사용 여부
        """
        self.src_path = path
        self.src_dir = src_dir
        self.dest_dir = dest_dir
        self.use_directory_urls = use_directory_urls
    
    @property
    def url(self):
        """
        파일 URL 반환
        
        Returns:
            str: 파일 URL
        """
        pass
    
    def is_documentation_page(self):
        """
        문서 페이지인지 확인
        
        Returns:
            bool: 문서 페이지 여부
        """
        pass
```

### Page 클래스

페이지 정보를 관리합니다.

```python
from mkdocs.structure.pages import Page

class Page:
    """페이지 클래스"""
    
    def __init__(self, title, file, config):
        """
        페이지 초기화
        
        Args:
            title (str): 페이지 제목
            file (File): 파일 객체
            config (Config): 설정 객체
        """
        self.title = title
        self.file = file
        self.config = config
        self.content = None
        self.meta = {}
    
    def read_source(self, config):
        """
        소스 파일 읽기
        
        Args:
            config (Config): 설정 객체
        """
        pass
    
    def render(self, config, files):
        """
        페이지 렌더링
        
        Args:
            config (Config): 설정 객체
            files (Files): 파일 목록
        """
        pass
```

## 🔌 플러그인 개발

### BasePlugin 클래스

모든 플러그인의 기본 클래스입니다.

```python
from mkdocs.plugins import BasePlugin
from mkdocs.config import config_options

class MyPlugin(BasePlugin):
    """커스텀 플러그인 예제"""
    
    # 플러그인 설정 정의
    config_scheme = (
        ('enabled', config_options.Type(bool, default=True)),
        ('option1', config_options.Type(str, default='default_value')),
        ('option2', config_options.Type(int, default=10)),
    )
    
    def on_config(self, config):
        """
        설정 로드 시 실행
        
        Args:
            config (Config): MkDocs 설정
            
        Returns:
            Config: 수정된 설정
        """
        if not self.config['enabled']:
            return config
            
        # 설정 수정 로직
        return config
    
    def on_files(self, files, config):
        """
        파일 목록 처리
        
        Args:
            files (Files): 파일 목록
            config (Config): 설정
            
        Returns:
            Files: 수정된 파일 목록
        """
        return files
    
    def on_page_markdown(self, markdown, page, config, files):
        """
        마크다운 처리
        
        Args:
            markdown (str): 마크다운 내용
            page (Page): 페이지 객체
            config (Config): 설정
            files (Files): 파일 목록
            
        Returns:
            str: 수정된 마크다운
        """
        # 마크다운 수정 로직
        return markdown
    
    def on_page_content(self, html, page, config, files):
        """
        HTML 콘텐츠 처리
        
        Args:
            html (str): HTML 내용
            page (Page): 페이지 객체
            config (Config): 설정
            files (Files): 파일 목록
            
        Returns:
            str: 수정된 HTML
        """
        return html
```

**플러그인 등록:**
```python
# setup.py
from setuptools import setup

setup(
    name='my-mkdocs-plugin',
    version='1.0.0',
    entry_points={
        'mkdocs.plugins': [
            'myplugin = myplugin:MyPlugin',
        ]
    },
    install_requires=['mkdocs>=1.0.0'],
)
```

### 플러그인 이벤트 순서

```python
class PluginEventOrder(BasePlugin):
    """플러그인 이벤트 실행 순서 예제"""
    
    def on_startup(self, command, dirty):
        """1. 시작 시 실행"""
        pass
    
    def on_shutdown(self):
        """마지막. 종료 시 실행"""
        pass
    
    def on_serve(self, server, config, builder):
        """개발 서버 시작 시"""
        pass
    
    def on_config(self, config):
        """2. 설정 로드 후"""
        return config
    
    def on_pre_build(self, config):
        """3. 빌드 시작 전"""
        pass
    
    def on_files(self, files, config):
        """4. 파일 목록 생성 후"""
        return files
    
    def on_nav(self, nav, config, files):
        """5. 네비게이션 생성 후"""
        return nav
    
    def on_env(self, env, config, files):
        """6. Jinja2 환경 생성 후"""
        return env
    
    def on_post_build(self, config):
        """빌드 완료 후"""
        pass
```

## 🎨 테마 개발

### 테마 구조

```
my-theme/
├── __init__.py
├── main.html
├── 404.html
├── base.html
├── content.html
├── nav.html
├── search.html
├── css/
│   └── theme.css
├── js/
│   └── theme.js
└── fonts/
    └── font.woff2
```

### BaseTheme 클래스

```python
from mkdocs.theme import Theme

class CustomTheme(Theme):
    """커스텀 테마 클래스"""
    
    def __init__(self):
        super().__init__('custom-theme')
    
    def get_env(self):
        """Jinja2 환경 커스터마이징"""
        env = super().get_env()
        
        # 커스텀 필터 추가
        env.filters['my_filter'] = self.my_filter
        
        # 전역 함수 추가
        env.globals['my_function'] = self.my_function
        
        return env
    
    def my_filter(self, value):
        """커스텀 Jinja2 필터"""
        return value.upper()
    
    def my_function(self):
        """커스텀 전역 함수"""
        return "Hello from theme!"
```

## 🔧 유틸리티 함수

### 파일 관련 유틸리티

```python
from mkdocs.utils import get_relative_url, normalize_url

# 상대 URL 생성
relative_url = get_relative_url('current/page.html', 'target/page.html')

# URL 정규화
normalized = normalize_url('path//to//file.html')
```

### 메타데이터 처리

```python
from mkdocs.utils import meta

# 메타데이터 파싱
with open('page.md', 'r', encoding='utf-8') as f:
    content = f.read()

metadata, content = meta.get_data(content)
```

### 로깅

```python
import logging
from mkdocs.config import config_options

# 로거 설정
log = logging.getLogger(__name__)

class MyPlugin(BasePlugin):
    def on_page_markdown(self, markdown, page, config, files):
        log.info(f"Processing page: {page.title}")
        log.debug(f"Content length: {len(markdown)}")
        log.warning("This is a warning")
        
        return markdown
```

## 🧪 테스트 유틸리티

### 플러그인 테스트

```python
import unittest
from mkdocs.config import Config
from mkdocs.structure.pages import Page
from mkdocs.structure.files import File

class TestMyPlugin(unittest.TestCase):
    
    def setUp(self):
        self.plugin = MyPlugin()
        self.config = Config(schema=())
        
    def test_plugin_config(self):
        """플러그인 설정 테스트"""
        config = {
            'enabled': True,
            'option1': 'test_value'
        }
        
        errors, warnings = self.plugin.load_config(config)
        self.assertEqual(len(errors), 0)
        self.assertEqual(self.plugin.config['option1'], 'test_value')
    
    def test_markdown_processing(self):
        """마크다운 처리 테스트"""
        markdown = "# Test Page\n\nContent here."
        page = Page('Test', None, self.config)
        
        result = self.plugin.on_page_markdown(
            markdown, page, self.config, None
        )
        
        self.assertIsInstance(result, str)
        self.assertIn('Test Page', result)

if __name__ == '__main__':
    unittest.main()
```

## 📚 실제 사용 예제

### 커스텀 매크로 플러그인

```python
import re
from mkdocs.plugins import BasePlugin

class MacroPlugin(BasePlugin):
    """매크로 확장 플러그인"""
    
    config_scheme = (
        ('macros', config_options.Type(dict, default={})),
    )
    
    def on_page_markdown(self, markdown, page, config, files):
        """매크로를 실제 내용으로 치환"""
        
        # 기본 매크로
        macros = {
            '{{version}}': config.get('extra', {}).get('version', '1.0.0'),
            '{{site_name}}': config['site_name'],
            '{{today}}': datetime.now().strftime('%Y-%m-%d'),
        }
        
        # 사용자 정의 매크로 추가
        macros.update(self.config.get('macros', {}))
        
        # 매크로 치환
        for macro, value in macros.items():
            markdown = markdown.replace(macro, str(value))
        
        return markdown
```

### SEO 최적화 플러그인

```python
from bs4 import BeautifulSoup

class SEOPlugin(BasePlugin):
    """SEO 최적화 플러그인"""
    
    def on_page_content(self, html, page, config, files):
        """HTML에 SEO 메타태그 추가"""
        
        soup = BeautifulSoup(html, 'html.parser')
        
        # 메타 description 추가
        if page.meta.get('description'):
            meta_desc = soup.new_tag('meta')
            meta_desc.attrs['name'] = 'description'
            meta_desc.attrs['content'] = page.meta['description']
            
            head = soup.find('head')
            if head:
                head.append(meta_desc)
        
        # Open Graph 태그 추가
        if page.meta.get('og_title'):
            og_title = soup.new_tag('meta')
            og_title.attrs['property'] = 'og:title'
            og_title.attrs['content'] = page.meta['og_title']
            
            head = soup.find('head')
            if head:
                head.append(og_title)
        
        return str(soup)
```

이러한 클래스와 메서드를 활용하여 강력한 MkDocs 확장을 개발할 수 있습니다! 🚀