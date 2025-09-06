# 배포 가이드

## GitHub Pages (추천)

가장 인기 있는 무료 호스팅 서비스입니다.

### 수동 배포
```bash
mkdocs gh-deploy
```

### 자동 배포 (GitHub Actions)
`.github/workflows/ci.yml` 파일을 생성하세요:

```yaml
name: ci
on:
  push:
    branches:
      - master
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Configure Git Credentials
        run: |
          git config user.name github-actions[bot]
          git config user.email 41898282+github-actions[bot]@users.noreply.github.com
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - run: pip install mkdocs-material
      - run: mkdocs gh-deploy --force
```

## Netlify

### 방법 1: Git 연동
1. Netlify에서 저장소 연결
2. Build command: `pip install mkdocs-material && mkdocs build`
3. Publish directory: `site`

### 방법 2: 수동 업로드
```bash
mkdocs build
# site 폴더를 Netlify에 업로드
```

## Vercel

`vercel.json` 파일 생성:
```json
{
  "buildCommand": "pip install mkdocs-material && mkdocs build",
  "outputDirectory": "site"
}
```

## 사용자 정의 도메인

### GitHub Pages
1. 저장소 Settings → Pages → Custom domain
2. 도메인 입력 (예: docs.mycompany.com)
3. DNS 설정에서 CNAME 레코드 추가

### DNS 설정 예시
```
Type: CNAME
Name: docs
Value: username.github.io
```

## 배포 전 체크리스트

- [ ] `site_url` 정확히 설정
- [ ] 모든 링크 확인
- [ ] 이미지 경로 확인
- [ ] 404 페이지 테스트
- [ ] 모바일 표시 확인

!!! success "배포 완료"
    이제 전 세계에서 당신의 문서에 접근할 수 있습니다! 🎉