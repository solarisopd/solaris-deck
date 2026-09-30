# SOLARIS OPPIDUM 발표 사이트 (Quarto)

CL-Link 투자설명자료(IM) · 동적담보관리(DCM) · 스탁론 사업 참여 제안(uic) 세 개의 reveal.js 슬라이드를
하나의 사이트로 묶어 GitHub Pages(public)로 배포한다.
WordPress Docs 메뉴에서 각 URL을 링크하면, 구성원이 클릭 → 슬라이드 발표가 가능하다.

## 구조

```
solaris-deck/
├─ _quarto.yml                  # 사이트 설정 (랜딩 + 덱)
├─ CNAME                        # 사용자 도메인 docs.solarisoppidum.com
├─ theme/solaris.scss           # 공용 디자인 토큰 (chain.link 톤) — im · dcm
├─ theme/uic.scss               # uic 덱 전용 최소 테마 (생성물)
├─ index.qmd                    # 랜딩(덱 진입 카드). uic 는 비공개 덱이라 카드를 두지 않는다
├─ im/index.qmd                 # INVESTMENT MEMORANDUM
├─ dcm/index.qmd                # Dynamic Collateral Management
├─ uic/index.qmd                # CL-Link 스탁론 사업 참여 제안 (14쪽, 생성물 — 직접 고치지 않는다)
├─ uic/uic-pages.css            # uic 쪽 디자인 (생성물)
├─ uic/uic-motion.html          # uic 그래픽 움직임(쪽2·5·9·12) — 손으로 관리하는 원본
├─ assets/uic/                  # uic 표지·뒷표지·라벨 SVG
├─ assets/slide6.html           # 임베드 다이어그램
└─ .github/workflows/publish.yml
```

> uic 의 `index.qmd` · `uic-pages.css` · `theme/uic.scss` 는 인쇄 원고에서 만든 생성물이다.
> 문구·디자인을 고칠 때는 생성 도구(`build_uic.py`)나 `uic/uic-motion.html` 을 고치고 다시 생성한다.

배포 후 URL (운영 도메인은 `CNAME` 의 `docs.solarisoppidum.com`):
- 랜딩 : `https://docs.solarisoppidum.com/`
- IM   : `https://docs.solarisoppidum.com/im/`
- DCM  : `https://docs.solarisoppidum.com/dcm/`
- uic  : `https://docs.solarisoppidum.com/uic/`  (쪽12 바로가기: `.../uic/#/13`)

---

## 1. 로컬 준비 (최초 1회)

1. Quarto 설치 — https://quarto.org/docs/get-started/ 에서 OS별 설치
2. 설치 확인
   ```bash
   quarto --version
   ```

## 2. 로컬 미리보기

1. 프로젝트 폴더로 이동
   ```bash
   cd solaris-deck
   ```
2. 미리보기 (브라우저 자동 실행, 저장 시 자동 새로고침)
   ```bash
   quarto preview
   ```
3. 전체 렌더만 할 경우
   ```bash
   quarto render
   ```
   결과물은 `_site/` 에 생성된다.

## 3. GitHub 저장소 생성 및 최초 push

1. GitHub 웹에서 **public** 저장소 생성 (이름: `solaris-deck`)
2. 로컬에서 Git 초기화 및 연결 (`<id>`는 본인 계정)
   ```bash
   cd solaris-deck
   git init
   git add .
   git commit -m "init: solaris deck (IM + DCM)"
   git branch -M main
   git remote add origin https://github.com/<id>/solaris-deck.git
   git push -u origin main
   ```

## 4. 최초 1회 로컬 배포 (gh-pages 브랜치 생성)

Actions가 동작하려면 `gh-pages` 브랜치가 먼저 있어야 한다. 최초 1회만:

1. 로컬에서 실행
   ```bash
   quarto publish gh-pages
   ```
2. 안내에 따라 진행하면 `gh-pages` 브랜치가 생성되고 첫 배포가 이뤄진다.

## 5. Pages 소스 설정

1. GitHub 저장소 → `Settings` → `Pages`
2. `Build and deployment` → `Source` 를 **Deploy from a branch** 로 두고
   `Branch` 를 **gh-pages / (root)** 로 지정 → `Save`

## 6. 이후 자동 배포

`main` 브랜치에 push할 때마다 `.github/workflows/publish.yml` 이
자동으로 렌더 → `gh-pages` 갱신 → 사이트 반영한다.

```bash
git add .
git commit -m "update slides"
git push
```

## 7. WordPress Docs 메뉴 연결

WordPress 관리자 → 메뉴 → 사용자 정의 링크로 추가:

| 메뉴 이름 | URL |
|-----------|-----|
| INVESTMENT MEMORANDUM | `https://docs.solarisoppidum.com/im/` |
| Dynamic Collateral Management | `https://docs.solarisoppidum.com/dcm/` |
| CL-Link 스탁론 사업 참여 제안 | `https://docs.solarisoppidum.com/uic/` |

- 각 항목의 **링크 대상을 "새 탭"** 으로 두면 발표 중 WordPress 화면이 그대로 남아 돌아가기 쉽다
  (메뉴 화면 오른쪽 위 "화면 옵션"에서 "링크 대상"을 켜야 보인다).
- uic 는 검색 노출을 막아 두었다(`noindex,nofollow`). 랜딩 페이지에도 카드를 두지 않는다 — **링크를 아는 사람만** 들어온다.
- ⚠ 이 사이트는 GitHub Pages(public)라 **WordPress 메뉴는 링크를 보이게/숨기게 할 뿐 접근을 막지 못한다.**
  주소를 아는 사람은 메뉴 없이도 열 수 있다. 접근 제한이 필요하면 별도 조치(비밀번호·로그인 등)가 필요하다.
- 같은 사이트 안에서는 덱 간 이동이 없다(uic 뒷표지의 ADMIN · CUSTOM 버튼은 CL-Link 사이트로 나가는 새 탭 링크).

---

## 발표 조작법 (reveal.js)

- 좌우 화살표 / Space : 슬라이드 이동
- `F` : 전체화면, `Esc` : 슬라이드 개요(그리드)
- `S` : 발표자 노트 창
- `?` : 단축키 도움말

## 호스팅 없이 파일로 발표 (대안)

`quarto render` 후 `_site/im/index.html` 을 브라우저로 직접 열어도 발표된다.
인터넷 배포가 곤란할 때 사용.

---

## 다음 작업 (콘텐츠)

- `im/index.qmd` : 현재 4개 샘플 슬라이드 → 15쪽으로 확장 (파일 하단 주석 참조)
- `assets/` : Octopus N:1 다이어그램(slide3.html) 추가 후 IM에 임베드
- 디자인 토큰 변경은 `theme/solaris.scss` 한 곳만 수정하면 두 덱에 일괄 적용
