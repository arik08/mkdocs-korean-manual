# CLI 명령어 참조

## 📋 개요

MkDocs는 명령줄 인터페이스(CLI)를 통해 다양한 작업을 수행할 수 있습니다. 이 문서는 모든 MkDocs 명령어와 옵션을 상세히 설명합니다.

## 🚀 기본 명령어

### mkdocs new

새로운 MkDocs 프로젝트를 생성합니다.

```bash
mkdocs new [프로젝트명]
```

**옵션:**
- 없음

**예제:**
```bash
mkdocs new my-project
mkdocs new docs-site
```

**생성되는 구조:**
```
my-project/
├── docs/
│   └── index.md
└── mkdocs.yml
```

### mkdocs serve

개발 서버를 시작합니다.

```bash
mkdocs serve [옵션]
```

**주요 옵션:**
- `-a, --dev-addr <IP:PORT>`: 서버 주소 설정 (기본: 127.0.0.1:8000)
- `-f, --config-file <파일>`: 설정 파일 지정
- `-s, --strict`: 경고를 오류로 처리
- `-t, --theme <테마>`: 테마 지정
- `--livereload/--no-livereload`: 라이브 리로드 설정
- `-w, --watch <경로>`: 추가 감시 경로
- `-q, --quiet`: 조용한 모드
- `-v, --verbose`: 상세한 로그

**예제:**
```bash
# 기본 실행
mkdocs serve

# 다른 포트에서 실행
mkdocs serve -a localhost:3000

# 외부 접속 허용
mkdocs serve -a 0.0.0.0:8000

# 추가 디렉토리 감시
mkdocs serve -w includes/

# 조용한 모드로 실행
mkdocs serve --quiet
```

### mkdocs build

정적 사이트를 빌드합니다.

```bash
mkdocs build [옵션]
```

**주요 옵션:**
- `-f, --config-file <파일>`: 설정 파일 지정
- `-c, --clean`: 빌드 전에 사이트 디렉토리 정리
- `-d, --site-dir <디렉토리>`: 출력 디렉토리 지정
- `-s, --strict`: 경고를 오류로 처리
- `-t, --theme <테마>`: 테마 지정
- `-q, --quiet`: 조용한 모드
- `-v, --verbose`: 상세한 로그

**예제:**
```bash
# 기본 빌드
mkdocs build

# 깔끔한 빌드 (기존 파일 삭제)
mkdocs build --clean

# 다른 출력 디렉토리
mkdocs build --site-dir ../output

# 엄격 모드 (경고시 실패)
mkdocs build --strict
```

### mkdocs gh-deploy

GitHub Pages에 배포합니다.

```bash
mkdocs gh-deploy [옵션]
```

**주요 옵션:**
- `-f, --config-file <파일>`: 설정 파일 지정
- `-b, --remote-branch <브랜치>`: 배포 브랜치 (기본: gh-pages)
- `-r, --remote-name <이름>`: 원격 저장소 이름 (기본: origin)
- `--force`: 강제 푸시
- `--ignore-version`: 버전 확인 무시
- `-m, --message <메시지>`: 커밋 메시지
- `--no-jekyll`: .nojekyll 파일 생성
- `-c, --clean`: 빌드 전에 정리
- `-s, --strict`: 엄격 모드
- `-q, --quiet`: 조용한 모드
- `-v, --verbose`: 상세한 로그

**예제:**
```bash
# 기본 배포
mkdocs gh-deploy

# 커스텀 커밋 메시지
mkdocs gh-deploy -m "Update documentation v1.2.0"

# 다른 브랜치에 배포
mkdocs gh-deploy -b docs-branch

# 강제 푸시
mkdocs gh-deploy --force

# 깔끔한 빌드 후 배포
mkdocs gh-deploy --clean
```

## 🔧 고급 명령어

### mkdocs get-deps

의존성을 확인하고 설치합니다.

```bash
mkdocs get-deps [옵션]
```

**옵션:**
- `-f, --config-file <파일>`: 설정 파일 지정
- `-q, --quiet`: 조용한 모드
- `-v, --verbose`: 상세한 로그

**예제:**
```bash
# 의존성 확인
mkdocs get-deps

# 특정 설정 파일 사용
mkdocs get-deps -f custom-mkdocs.yml
```

## 📊 유틸리티 명령어

### --version

MkDocs 버전을 확인합니다.

```bash
mkdocs --version
```

### --help

도움말을 표시합니다.

```bash
mkdocs --help
mkdocs serve --help
mkdocs build --help
```

## 🔄 워크플로우 예제

### 개발 워크플로우

```bash
# 1. 새 프로젝트 생성
mkdocs new my-docs

# 2. 디렉토리 이동
cd my-docs

# 3. 개발 서버 시작
mkdocs serve

# 4. 다른 터미널에서 빌드 테스트
mkdocs build --clean --strict

# 5. GitHub Pages 배포
mkdocs gh-deploy
```

### CI/CD 스크립트

```bash
#!/bin/bash
# build-and-deploy.sh

set -e  # 오류 시 스크립트 중단

echo "MkDocs 의존성 확인 중..."
mkdocs get-deps

echo "사이트 빌드 중..."
mkdocs build --clean --strict --verbose

echo "빌드 결과 확인 중..."
if [ ! -d "site" ]; then
    echo "빌드 실패: site 디렉토리가 없습니다."
    exit 1
fi

echo "GitHub Pages에 배포 중..."
mkdocs gh-deploy --clean --message "Deployed by CI/CD at $(date)"

echo "배포 완료!"
```

### 배치 빌드 스크립트

```bash
#!/bin/bash
# multi-build.sh

# 다양한 환경에서 빌드
CONFIGS=("mkdocs.yml" "mkdocs-dev.yml" "mkdocs-prod.yml")

for config in "${CONFIGS[@]}"; do
    echo "Building with $config..."
    if mkdocs build -f "$config" --clean --site-dir "site-$(basename $config .yml)"; then
        echo "✅ $config 빌드 성공"
    else
        echo "❌ $config 빌드 실패"
        exit 1
    fi
done

echo "모든 빌드 완료!"
```

## 🎯 고급 사용법

### 환경 변수 활용

```bash
# 환경별 설정
export MKDOCS_CONFIG_FILE=mkdocs-production.yml
export MKDOCS_SITE_URL=https://docs.mycompany.com
export MKDOCS_STRICT_MODE=true

# 빌드 실행
mkdocs build \
  --config-file "${MKDOCS_CONFIG_FILE}" \
  --site-dir "dist" \
  $([ "$MKDOCS_STRICT_MODE" = "true" ] && echo "--strict") \
  --clean
```

### 조건부 실행

```bash
# 파일 변경 감지 후 빌드
if [ docs/ -nt site/ ]; then
    echo "문서가 변경되었습니다. 리빌드합니다."
    mkdocs build --clean
else
    echo "문서에 변경사항이 없습니다."
fi
```

### 멀티플랫폼 스크립트

```bash
#!/bin/bash
# cross-platform-build.sh

# 운영체제 감지
case "$OSTYPE" in
  linux-gnu*|cygwin|msys)
    PYTHON_CMD="python3"
    ;;
  darwin*)
    PYTHON_CMD="python3"
    ;;
  win32|win64)
    PYTHON_CMD="python"
    ;;
  *)
    echo "지원하지 않는 운영체제: $OSTYPE"
    exit 1
    ;;
esac

# MkDocs 실행
$PYTHON_CMD -m mkdocs build --clean
```

## 🔍 문제 해결

### 일반적인 오류와 해결책

**오류**: `Config file 'mkdocs.yml' does not exist.`
```bash
# 현재 디렉토리 확인
pwd
ls -la

# 올바른 디렉토리로 이동
cd /path/to/your/mkdocs/project
```

**오류**: `Address already in use`
```bash
# 다른 포트 사용
mkdocs serve -a localhost:8001

# 또는 실행 중인 프로세스 종료
lsof -ti:8000 | xargs kill -9
```

**오류**: `No module named 'mkdocs'`
```bash
# MkDocs 설치
pip install mkdocs mkdocs-material

# 가상환경 확인
which python
which mkdocs
```

### 디버깅 옵션

```bash
# 상세한 로그로 실행
mkdocs serve --verbose

# 설정 파일 검증
mkdocs build --strict --dry-run

# 의존성 문제 해결
mkdocs get-deps --verbose
```

## 📚 명령어 치트시트

| 명령어 | 기능 | 주요 옵션 |
|--------|------|-----------|
| `mkdocs new <name>` | 새 프로젝트 생성 | - |
| `mkdocs serve` | 개발 서버 시작 | `-a`, `--livereload`, `-w` |
| `mkdocs build` | 정적 사이트 빌드 | `--clean`, `--strict`, `-d` |
| `mkdocs gh-deploy` | GitHub Pages 배포 | `--force`, `-m`, `-b` |
| `mkdocs get-deps` | 의존성 확인 | `-f` |
| `mkdocs --version` | 버전 확인 | - |
| `mkdocs --help` | 도움말 | - |

이제 MkDocs CLI를 완전히 활용할 수 있습니다! 🚀