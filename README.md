# 총학생회장의 리포트

BigSub 선생님과 총학쨩이 함께 만든 리서치·분석 리포트를 모아두는 GitHub Pages 포털입니다.

- 공개 포털: https://fetitronik-ops.github.io/presidentchanspages/
- GitHub repo: https://github.com/fetitronik-ops/presidentchanspages

## 페이지 컨셉

루트 `index.html`은 “총학생회장의 리포트”라는 이름의 리포트 아카이브 홈입니다.

디자인 방향:

- 화이트 문서지 / 결재서류 느낌
- 연한 핑크와 연한 하늘색 중심
- `Federal Investigation Club` / `S.C.H.A.L.E` 라벨
- 총학쨩 프로필 이미지가 포함된 헤더
- 리포트 카드는 결재 문서 목록처럼 표시

## 현재 파일 구조

```text
/
  index.html
  headerimage.png
  README.md
  .nojekyll

  data/
    reports.json

  reports/
    azur-promilia-vs-project-rx/
      index.html
      assets/
        azur_promilia_hero.jpg
        project_rx_hero.jpg
```

## 주요 파일 설명

### `index.html`

포털의 루트 페이지입니다.

역할:

- `data/reports.json`을 읽어서 리포트 카드 목록을 렌더링합니다.
- 리포트 제목, 날짜, 카테고리, 요약, 링크를 표시합니다.
- 키워드/tag pill은 표시하지 않습니다.
- 로컬 단독 미리보기를 위해 `data/reports.json` 로딩 실패 시 샘플 데이터 fallback을 포함합니다.

### `headerimage.png`

루트 포털 헤더에 표시되는 총학쨩 이미지입니다.

현재 표시 방식:

- 왼쪽 정렬
- 둥근 꼭짓점
- 그림자 없음
- 정사각형 카드형 이미지

### `data/reports.json`

포털에 표시할 리포트 목록 메타데이터입니다.

현재 스키마:

```json
[
  {
    "slug": "azur-promilia-vs-project-rx",
    "title": "아주르 프로밀리아 vs Project RX 국내 버즈량 확장 비교",
    "date": "2026-05-16",
    "category": "버즈 분석",
    "summary": "아카라이브, 디시, 루리웹, 게임웹진, YouTube, X/검색 노출을 확장 비교한 국내 버즈량 리포트입니다.",
    "url": "reports/azur-promilia-vs-project-rx/"
  }
]
```

필드 설명:

- `slug`: 리포트 식별자이자 폴더명
- `title`: 포털 카드에 표시할 제목
- `date`: 작성일 또는 발행일
- `category`: 리포트 분류
- `summary`: 포털 카드에 표시할 한 줄/짧은 요약
- `url`: 개별 리포트 페이지 경로

현재는 `tags` 필드를 사용하지 않습니다.

### `reports/<slug>/index.html`

개별 리포트 본문 페이지입니다.

각 리포트는 고유 slug 폴더를 갖습니다.

예:

```text
reports/azur-promilia-vs-project-rx/index.html
```

### `reports/<slug>/assets/`

개별 리포트에 필요한 이미지/첨부 리소스를 넣는 폴더입니다.

리포트 HTML 안에서는 상대 경로로 참조합니다.

예:

```html
<img src="assets/azur_promilia_hero.jpg" alt="...">
```

### `.nojekyll`

GitHub Pages가 Jekyll 처리를 하지 않고 정적 파일을 그대로 서빙하도록 하는 파일입니다.

## 새 리포트 추가 절차

1. 새 리포트 slug를 정합니다.

예:

```text
blue-archive-kr-ost-demand
```

2. 리포트 폴더를 만듭니다.

```text
reports/blue-archive-kr-ost-demand/
```

3. 리포트 HTML을 배치합니다.

```text
reports/blue-archive-kr-ost-demand/index.html
```

4. 이미지가 있으면 assets 폴더에 넣습니다.

```text
reports/blue-archive-kr-ost-demand/assets/
```

5. `data/reports.json`에 항목을 추가합니다.

```json
{
  "slug": "blue-archive-kr-ost-demand",
  "title": "블루 아카이브 한국 OST 인게임 수요 조사",
  "date": "2026-05-16",
  "category": "수요 조사",
  "summary": "커뮤니티와 유튜브 반응을 기반으로 한국 OST의 인게임 수요를 정리한 리포트입니다.",
  "url": "reports/blue-archive-kr-ost-demand/"
}
```

6. GitHub에 업로드합니다.

BigSubClaw는 로컬 PAT를 사용해 GitHub API로 업로드합니다.

토큰 위치:

```text
~/.config/github/bigsubclaw_reports_token
```

권한:

```text
600
```

기본 업데이트에는 보통 `Contents: Read and write` 권한이면 충분합니다.

## GitHub Pages 설정

현재 Pages는 다음 방식으로 활성화되어 있습니다.

```text
Source: Deploy from a branch
Branch: main
Folder: /root
```

Pages 최초 활성화 API에는 `pages=write` 외에 `administration=write` 권한도 요구될 수 있습니다. 이미 Pages가 활성화된 뒤에는 일반 파일 업데이트만으로 포털이 갱신됩니다.

## 현재 수록 리포트

1. 아주르 프로밀리아 vs Project RX 국내 버즈량 확장 비교
   - URL: https://fetitronik-ops.github.io/presidentchanspages/reports/azur-promilia-vs-project-rx/
   - Category: 버즈 분석
   - Date: 2026-05-16

## 운영 메모

- 루트 포털 디자인은 `/index.html`에서 관리합니다.
- 리포트 목록은 `/data/reports.json`에서 관리합니다.
- 개별 리포트는 `/reports/<slug>/` 아래에 독립적으로 둡니다.
- 리포트가 많아지면 나중에 검색, 카테고리 필터, 연도별 그룹을 `index.html`에 추가하면 됩니다.
