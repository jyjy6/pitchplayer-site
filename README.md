# PitchPlayer Site

PitchPlayer 앱 소개 및 GitHub Pages 배포용 웹사이트입니다.

## 주요 목적
1. Google AdMob `app-ads.txt` 호스팅 (`/app-ads.txt`)
2. PitchPlayer 랜딩 페이지 및 개인정보처리방침 안내

## 로컬 개발 및 빌드

```bash
# 디렉토리 이동
cd pitchplayer-site

# 패키지 설치
npm install

# 개발 서버 실행
npm run dev

# GitHub Pages용 빌드
npm run build
```

빌드 결과물은 `dist/` 폴더에 생성됩니다.
GitHub Pages 설정 시 `gh-pages` 브랜치에 `dist/` 내용을 배포하거나 GitHub Actions를 활용할 수 있습니다.
