# 문제 해결 가이드

## 일반적인 문제들

### 1. 설치 및 환경 문제

#### Python 버전 호환성
```bash
# Python 버전 확인
python --version

# MkDocs는 Python 3.7 이상 필요
```

#### pip 설치 문제
```bash
# pip 업그레이드
python -m pip install --upgrade pip

# 권한 문제 시 (Windows)
pip install --user mkdocs-material

# 가상환경 사용 권장
python -m venv mkdocs-env
```

### 2. 빌드 오류

#### YAML 구문 오류
```yaml
# 올바른 예시
nav:
  - 홈: index.md
  - 가이드: guide.md
```

**해결법:**
- 들여쓰기는 공백 2칸 사용
- 콜론(:) 뒤에 반드시 공백 추가

#### 파일 경로 오류
```bash
# 오류 메시지 예시
WARNING - The following pages exist in the docs directory, but are not 
          included in the "nav" configuration

# 해결법: 네비게이션에 추가
nav:
  - 홈: index.md
  - 누락된 페이지: missing-page.md
```

### 3. 테마 관련 문제

#### Material 테마가 적용되지 않음
```bash
# Material 테마 재설치
pip uninstall mkdocs-material
pip install mkdocs-material

# 설정 확인
theme:
  name: material  # 'Material'이 아닌 'material'
```

#### 커스텀 CSS가 적용되지 않음
```yaml
# 올바른 설정
extra_css:
  - assets/stylesheets/extra.css  # docs/ 기준 상대 경로
```

### 4. 성능 문제

#### 빌드 속도 느림
```yaml
# 개발 시 최적화 비활성화
plugins:
  - search:
      prebuild_index: false  # 개발 시 false
```

#### 검색 속도 느림
```yaml
plugins:
  - search:
      lang: ko
      indexing: sections    # full 대신 sections
```

## 자주 묻는 질문 (FAQ)

### Q: 한글 파일명을 사용할 수 있나요?
A: 가능하지만 권장하지 않습니다. URL에서 인코딩 문제가 발생할 수 있습니다.

### Q: 수학 공식이 표시되지 않아요
A: MathJax 설정을 확인하세요:
```yaml
markdown_extensions:
  - pymdownx.arithmatex:
      generic: true

extra_javascript:
  - https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js
```

### Q: 검색이 한글을 지원하지 않아요
A: 검색 언어를 한국어로 설정하세요:
```yaml
plugins:
  - search:
      lang: ko
```

## 빠른 체크리스트

문제가 발생했을 때 다음 순서로 확인해보세요:

- [ ] Python 버전 3.7 이상인가?
- [ ] MkDocs와 테마가 최신 버전인가?
- [ ] `mkdocs.yml` 문법이 올바른가?
- [ ] 파일 경로가 정확한가?
- [ ] 인코딩이 UTF-8인가?
- [ ] 필요한 플러그인이 설치되었는가?

이 체크리스트를 따라하면 대부분의 문제를 해결할 수 있습니다!