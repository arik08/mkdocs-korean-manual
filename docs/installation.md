# 설치 가이드

## 시스템 요구사항

MkDocs를 설치하기 전에 다음 요구사항을 확인하세요:

- **Python 3.7 이상**
- **pip** (Python 패키지 관리자)
- **Git** (선택사항, 버전 관리용)

## 설치 방법

### 1. 기본 설치

가장 간단한 방법으로 MkDocs를 설치합니다:

```bash
pip install mkdocs
```

### 2. Material 테마와 함께 설치

Material 테마를 포함하여 설치하는 것을 권장합니다:

```bash
pip install mkdocs-material
```

### 3. 추가 플러그인 설치

유용한 플러그인들을 함께 설치할 수 있습니다:

```bash
pip install mkdocs-material mkdocs-git-revision-date-localized-plugin mkdocs-minify-plugin
```

## 가상환경 사용 (권장)

프로젝트별로 독립된 환경을 사용하는 것을 권장합니다:

### Windows

```batch
# 가상환경 생성
python -m venv mkdocs-env

# 가상환경 활성화
mkdocs-env\Scripts\activate

# MkDocs 설치
pip install mkdocs-material
```

### macOS/Linux

```bash
# 가상환경 생성
python3 -m venv mkdocs-env

# 가상환경 활성화
source mkdocs-env/bin/activate

# MkDocs 설치
pip install mkdocs-material
```

## 설치 확인

설치가 완료되었는지 확인해보세요:

```bash
mkdocs --version
```

성공적으로 설치되었다면 버전 정보가 출력됩니다.

!!! success "설치 완료!"
    이제 MkDocs를 사용할 준비가 완료되었습니다!

## 다음 단계

설치가 완료되었다면:

1. [첫 번째 프로젝트 만들기](first-project.md)
2. [기본 설정 배우기](configuration.md)
3. [테마 적용하기](themes.md)