# 이나이에 Eenaie - 무지성 행동실화

> 40대 중년의 고분분투 항해일지

개인 블로그 사이트입니다. IT 업계에서 개발자부터 창업가까지 다양한 역할을 경험한 중년 전문가의 기술, AI, 커리어에 대한 이야기를 담고 있습니다.

🌐 **사이트**: [https://eenaie.com](https://eenaie.com)

## 기술 스택

- **정적 사이트 생성기**: [Hugo](https://gohugo.io/) (Extended v0.148.1+)
- **테마**: [Blowfish](https://github.com/nunocoracao/blowfish)
- **호스팅**: GitHub Pages
- **CI/CD**: GitHub Actions
- **언어**: 한국어 (Korean)

## 시작하기

### 사전 요구사항

- Hugo Extended 버전 설치 필요
- Git

### 설치

1. 저장소 클론 및 서브모듈 초기화:

```bash
git clone https://github.com/your-username/eenaie-blog.git
cd eenaie-blog
git submodule update --init --recursive
```

2. Hugo 설치 (macOS):

```bash
brew install hugo
```

다른 운영체제의 경우 [Hugo 공식 문서](https://gohugo.io/installation/)를 참고하세요.

3. Hugo Extended 버전 확인:

```bash
hugo version
# 출력에 'extended'가 포함되어야 합니다
```

### 로컬 개발 서버 실행

```bash
# 초안 포함하여 개발 서버 시작
hugo server -D

# 초안 제외하고 서버 시작
hugo server
```

브라우저에서 `http://localhost:1313/`로 접속하여 사이트를 확인할 수 있습니다.

## 콘텐츠 작성

### 새 블로그 포스트 작성

```bash
hugo new posts/<포스트-이름>/index.md
```

생성된 `content/posts/<포스트-이름>/index.md` 파일을 편집합니다:

```yaml
---
title: "포스트 제목"
date: 2025-07-17
draft: false  # 게시할 준비가 되면 false로 변경
slug: "url-친화적-슬러그"
description: "SEO 설명"
tags: ["태그1", "태그2"]
categories: ["카테고리1"]
---

여기에 콘텐츠를 작성합니다...
```

### 이미지 추가

- 포스트 이미지는 해당 포스트 디렉토리에 함께 저장합니다
- WebP 형식 권장
- Hugo shortcode 사용:

```markdown
{{< figure src="image.webp" alt="이미지 설명" caption="이미지 캡션" >}}
```

## 빌드 및 배포

### 로컬 빌드

```bash
hugo --minify --gc
```

빌드된 정적 파일은 `public/` 디렉토리에 생성됩니다.

### 자동 배포

`main` 브랜치에 push하면 GitHub Actions가 자동으로:
1. Hugo Extended로 사이트 빌드
2. GitHub Pages에 배포
3. 커스텀 도메인 (eenaie.com) 설정

배포 워크플로우는 `.github/workflows/deploy.yml`에서 확인할 수 있습니다.

## 프로젝트 구조

```
eenaie-blog/
├── .github/
│   └── workflows/
│       └── deploy.yml          # GitHub Actions 배포 설정
├── archetypes/
│   └── default.md              # 새 콘텐츠 템플릿
├── assets/
│   └── images/                 # 프로필 이미지 등
├── config/
│   └── _default/               # Hugo 설정 파일들
│       ├── hugo.toml           # 기본 Hugo 설정
│       ├── params.toml         # 테마 파라미터
│       ├── languages.ko.toml   # 한국어 설정
│       ├── menus.ko.toml       # 메뉴 설정
│       └── markup.toml         # 마크다운 설정
├── content/
│   ├── about/                  # 소개 페이지
│   └── posts/                  # 블로그 포스트들
│       └── <post-name>/
│           ├── index.md
│           └── *.webp
├── static/
│   └── CNAME                   # 커스텀 도메인 설정
├── themes/
│   └── blowfish/               # Blowfish 테마 (git submodule)
└── hugo.toml                   # Hugo 루트 설정
```

## 테마 업데이트

Blowfish 테마는 git submodule로 관리됩니다. 테마를 최신 버전으로 업데이트하려면:

```bash
cd themes/blowfish
git pull origin main
cd ../..
git add themes/blowfish
git commit -m "테마 업데이트"
```

## 설정

주요 설정 파일:
- **사이트 메타데이터**: `config/_default/languages.ko.toml`
- **테마 외관/기능**: `config/_default/params.toml`
- **네비게이션 메뉴**: `config/_default/menus.ko.toml`
- **분류 체계**: `config/_default/hugo.toml` (tags, categories, authors, series)

## 개발 팁

- 초안 작성 시 `draft: true`로 설정하여 프로덕션에 노출되지 않도록 합니다
- 로컬 개발 시 `hugo server -D` 사용하여 초안도 함께 확인할 수 있습니다
- 이미지는 WebP 형식 사용을 권장합니다 (성능 최적화)
- 마크다운 문법과 Hugo shortcode를 활용하여 풍부한 콘텐츠를 작성할 수 있습니다

## 저작권

© 2025 Dokahn Works, Inc. All rights reserved.

## 링크

- 🌐 블로그: [https://eenaie.com](https://eenaie.com)
- 📺 YouTube: [@eenaie](https://www.youtube.com/@eenaie)
- 🧵 Threads: [@eenaie](https://www.threads.com/@eenaie)
- 📷 Instagram: [@eenaie](https://www.instagram.com/eenaie)

---

Made with ❤️ using [Hugo](https://gohugo.io/) and [Blowfish](https://github.com/nunocoracao/blowfish)
