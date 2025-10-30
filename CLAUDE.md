# CLAUDE.md

이 파일은 Claude Code (claude.ai/code)가 이 저장소에서 작업할 때 참고하는 가이드입니다.

## 프로젝트 개요

Hugo 정적 사이트 생성기로 만든 개인 블로그입니다. Blowfish 테마를 사용하며, 기술, AI, 커리어 주제를 다룹니다. GitHub Pages로 배포되며 커스텀 도메인(eenaie.com)을 사용합니다.

**저자**: 이나이에 (Eenaie) - IT 업계를 항해하는 중년 전문가의 경험담
**기본 URL**: https://eenaie.com
**언어**: 한국어 (ko)
**테마**: Blowfish (`themes/blowfish/`에 git submodule로 포함)

## 필수 명령어

### 개발
```bash
# 로컬 개발 서버 시작 (초안 포함)
hugo server -D

# 초안 제외하고 서버 시작
hugo server

# 사이트 빌드 (public/ 디렉토리에 출력)
hugo --minify --gc
```

### 콘텐츠 생성
```bash
# 새 포스트 생성 (content/posts/ 에 생성됨)
hugo new posts/<포스트-이름>/index.md

# 아키타입 템플릿은 archetypes/default.md 참고
```

### 배포
`main` 브랜치에 push하면 `.github/workflows/deploy.yml`을 통해 자동으로 GitHub Pages에 배포됩니다. 워크플로우 과정:
1. 서브모듈 포함하여 코드 체크아웃 (테마용)
2. Hugo Extended 버전 설치
3. `hugo --minify --gc`로 빌드
4. `eenaie.com` 도메인으로 CNAME 파일 추가 (public/CNAME)
5. GitHub Pages에 배포

**참고**: 커스텀 도메인 설정은 `static/CNAME` 파일에 저장되어 있으며, GitHub Actions 워크플로우에서도 중복으로 public/CNAME에 추가합니다.

## 구조 및 설정

### Hugo 설정 구조
프로젝트는 `config/_default/` 디렉토리에 여러 설정 파일을 사용합니다:

- **hugo.toml**: 테마, 언어, 분류체계(taxonomies), 관련 콘텐츠 설정 등 핵심 Hugo 설정
- **params.toml**: Blowfish 테마 파라미터 (외관, 레이아웃, 기능)
- **languages.ko.toml**: 한국어 설정, 저자 소개, 사이트 메타데이터
- **menus.ko.toml**: 네비게이션 메뉴 설정
- **markup.toml**: 마크다운 렌더링 설정

루트의 `hugo.toml` 파일은 최소한의 내용만 있으며, `config/_default/` 구조를 우선적으로 사용합니다.

### 콘텐츠 구성

```
content/
├── about/              # 소개 페이지 (저자 프로필)
│   ├── index.md       # 페이지 내용
│   └── *.jpg          # 저자 이미지
└── posts/             # 블로그 포스트
    └── <포스트-이름>/  # 각 포스트는 별도 디렉토리
        ├── index.md   # 프론트매터가 포함된 포스트 내용
        └── *.webp     # 포스트 이미지/에셋
```

**포스트 프론트매터 구조**:
```yaml
---
title: "포스트 제목"
date: 2025-07-17
draft: false
slug: "url-친화적-슬러그"
description: "SEO 설명"
tags: ["태그1", "태그2"]
categories: ["카테고리1"]
---
```

### 테마 커스터마이징
Blowfish 테마는 git submodule로 포함되어 있습니다. `config/_default/params.toml`의 주요 테마 설정:
- 색상 스킴: "Fire", 기본 다크 모드
- 홈페이지 레이아웃: "profile" 스타일, 최근 포스트 표시
- 기능: 스마트 목차, 코드 복사 비활성화, 검색 활성화
- 아티클 설정: 날짜, 저자, 읽기 시간, 단어 수, 목차 표시

### 분류체계 (Taxonomies)
`config/_default/hugo.toml`에 설정된 여러 분류체계:
- `tags` - 포스트의 주제 태그
- `categories` - 포괄적인 콘텐츠 카테고리
- `authors` - 저자 구분 (다중 저자 지원)
- `series` - 연재 시리즈 그룹핑

## 콘텐츠 작업

### 새 포스트 만들기
1. 포스트는 `content/posts/` 하위의 개별 디렉토리로 구성
2. 각 포스트 디렉토리에는 `index.md`와 관련 에셋 포함
3. 이미지는 최적화를 위해 WebP 형식 사용
4. 포스트가 게시 준비되면 항상 `draft: false`로 설정

### 이미지 처리
- 프로필 이미지: `assets/images/`에 저장 (profile.webp, author.png 등)
- 포스트 이미지: 포스트의 `index.md`와 같은 디렉토리에 저장
- 성능을 위해 WebP 형식 권장
- 마크다운에서 경로 접두사 없이 참조: `![설명](image.webp)`
- Hugo shortcode 사용 예시: `{{< figure src="image.webp" alt="설명" caption="캡션" >}}`

### 콘텐츠 가이드라인 (기존 포스트 기반)
- 대상 독자: 기술에 관심 있는 한국어 사용 전문가
- 작성 스타일: 개인적이고 대화체, 경험 기반
- 실용적인 예시와 단계별 설명 포함
- 가독성을 위해 구조화된 제목과 불릿 포인트 사용

## Git 워크플로우

**현재 브랜치**: `main` (배포 브랜치이기도 함)

### 서브모듈
Blowfish 테마를 git submodule로 관리합니다:
- **저장소**: https://github.com/nunocoracao/blowfish.git
- **브랜치**: main
- **경로**: themes/blowfish

```bash
# 테마 서브모듈 초기화/업데이트
git submodule update --init --recursive

# 테마 업데이트
cd themes/blowfish
git pull origin main
cd ../..
git add themes/blowfish
git commit -m "테마 업데이트"
```

### 최근 활동
최근 커밋 내역:
- 프로필 이미지 업데이트
- 콘텐츠 개선
- 첫 블로그 포스트 작성
- 소개 페이지 설정
- 커스텀 도메인을 위한 CNAME 설정

## 개발 참고사항

### Hugo Extended 필수
Blowfish 테마의 의존성 때문에 이 프로젝트는 Hugo Extended 버전이 필요합니다 (표준 Hugo가 아님). Extended 버전은 SCSS/SASS 처리 기능을 포함합니다.

**설치된 버전**: Hugo v0.148.1+extended (Homebrew를 통해 설치됨)

Hugo 설치:
```bash
# macOS (Homebrew)
brew install hugo

# 버전 확인
hugo version
```

### 로컬 개발
`hugo server`로 로컬 실행 시 사이트는 `http://localhost:1313/`에서 접근 가능합니다. 초안 포스트는 `-D` 플래그 사용 시에만 보입니다.

### 빌드 출력
`public/` 디렉토리에 생성된 정적 사이트가 포함됩니다. 이 디렉토리는 gitignore되며 배포마다 재빌드됩니다.

### 리소스
Hugo는 리소스를 처리하고 `resources/_gen/` 디렉토리에 캐시합니다. 이것도 gitignore됩니다.

## 사이트 정체성

**사이트 제목**: 이나이에 Eenaie - 무지성 행동실화
**설명**: 40대 중년의 고분분투 항해일지
**저자 소개**: 호기심 많은 젊은이에서 어느덧 세상의 속도가 버거운 아저씨로...
**소셜 링크**: YouTube, Threads, Instagram (@eenaie)
**저작권**: © 2025 Dokahn Works, Inc.

이 컨텍스트는 콘텐츠를 생성하거나 수정할 때 사이트의 목소리와 콘텐츠 전략을 파악하는 데 도움이 됩니다.
