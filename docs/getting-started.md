# 시작하기

## MkDocs란?

MkDocs는 **빠르고**, **간단한**, **아름다운** 정적 사이트 생성기입니다. 프로젝트 문서를 만들기 위해 특별히 설계되었습니다.

## 주요 특징

- **Markdown으로 작성**: 간단한 Markdown 문법을 사용하여 문서를 작성할 수 있습니다.
- **실시간 미리보기**: `mkdocs serve` 명령으로 실시간으로 변경사항을 확인할 수 있습니다.
- **테마 지원**: 다양한 테마를 사용하여 사이트의 모양을 꾸밀 수 있습니다.
- **플러그인 확장**: 다양한 플러그인으로 기능을 확장할 수 있습니다.

## 설치 방법

```bash
pip install mkdocs
pip install mkdocs-material
```

## 기본 명령어

| 명령어 | 설명 |
|--------|------|
| `mkdocs new [프로젝트명]` | 새 프로젝트 생성 |
| `mkdocs serve` | 로컬 서버 실행 |
| `mkdocs build` | 정적 사이트 빌드 |
| `mkdocs gh-deploy` | GitHub Pages에 배포 |

!!! note "참고사항"
    MkDocs는 Python 3.6 이상에서 동작합니다.

!!! tip "팁"
    `mkdocs serve`를 사용하면 파일을 저장할 때마다 자동으로 브라우저가 새로고침됩니다.

## 다음 단계

1. [설치 가이드](installation.md)에서 자세한 설치 방법을 확인하세요
2. [첫 프로젝트](first-project.md)를 만들어보세요
3. [기본 설정](configuration.md)을 배워보세요