# solaris-deck/.ai/ — 프로젝트 인수인계

SOLARIS OPPIDUM 발표 사이트 (Quarto + reveal.js).
CL-Link 투자설명자료(IM)와 동적담보관리(DCM) 두 슬라이드를 하나의 사이트로 묶어
GitHub Pages(public)로 배포 → WordPress Docs 메뉴에서 링크.

- 레포: https://github.com/solarisopd/solaris-deck.git (계정: solarisopd / 기본 브랜치: main)
- 집 PC: G:\solaris-deck
- 배포 URL: https://solarisopd.github.io/solaris-deck/ (랜딩) · /im/ · /dcm/

## 현재 상태 (2026-06-07)
- 마지막: 2026-06-07 / Claude Code / 집 PC / 커밋 f382d7d
- **방침 전환(6/7): 전면 SVG화 폐기 → 이미지 도해 쪽만 SVG, 나머지는 마크다운.** IM 1~17쪽 전부 마크다운화 완료. 남은 `.svg-slide` 없음
  - 5·6쪽만 제목부 마크다운(`.diagram-head`) + 동적 도면(인라인 SVG 애니메이션) 보존. `slides/05·06.svg`(제목 오버레이)는 미사용. 나머지 `slides/NN.svg`는 되돌리기 대비 보존
- 페이지 규칙(3쪽 기준): 제목부 PART 배지(`.part-badge`)→페이지제목(`.page-title`)→설명(`.subtitle`) / 본문 `.md-body`(절대배치·세로중앙) / 하단 `.tagline` 참조부. 표 0.6em, 첫열 nowrap
  - 표 열폭은 마크다운 구분선 대시 비율로 제어(Pandoc colgroup). 3열 비교표는 `.ctrl-table`(table-layout:fixed)+`.wrap-cells`
  - 14쪽 좌우 2표 `.two-col.ts-cols`(상단정렬) / 11·17쪽 2카드 `.demo-cards`(옅은 배경 $region·0.6em·높이130%) / 목차 카드 `.toc-cards` 옅은 배경
  - PART 1 섹션명: "회사와 인프라"→"CL-Link 인프라"로 통일(3·4·5·6·7쪽·목차)
- 5·6쪽 도면 애니메이션: `.diagram-slide:not(.present)`일 때 `animation:none` → 슬라이드 진입 시 0%부터 재생(중간진입 방지)
- 텍스트 원칙: 본문 텍스트는 slide_ai SVG에 작성한 문구를 정본으로 사용(서술형 "-다/-이다" 어미 제거 등)
- DCM 덱 7쪽 완성 (dcm/index.qmd 158줄) — 미변경
- 주의: OneDrive `...\20260609PPT\solaris-deck\solaris-deck` 는 비-Git 구버전 사본 → 작업 금지, 최신본은 G:\solaris-deck

## IM 슬라이드 SVG 교체 규약
- 원본: `C:\Users\MRB\OneDrive\00솔라리스오피둠\20260609PPT\slide_ai\NN.svg` (01~17, 파일번호 = 쪽번호)
- 교체 방식: SVG를 `im/slides/NN.svg`로 복사 → `im/index.qmd`에서 `![](slides/NN.svg){.slide-art}` 임베드
- 슬라이드 헤딩: `## &nbsp; {.svg-slide data-menu-title="..."}`. 어두운(네이비) 아트워크는 `background-color="#1A2A66"` 추가(여백 이음매 제거)
- **공통 유지(사용자 고정 지시)**: 하단 copyright `<div class="confidential">…</div>`는 각 슬라이드 유지 / 쪽번호(reveal `slide-number:c/t`)·넘김버튼(`controls`)은 전역 자동 적용 — 건드리지 말 것
- CSS: theme/solaris.scss `.reveal section.svg-slide`(img.slide-art = absolute/inset:0/object-fit:contain) / frontmatter `auto-stretch:false` 필수(미설정 시 r-stretch가 풀블리드 깨뜨림)
- 진행: 2026-06-06 1~8·10~17쪽 완료(9쪽 제외, 09.svg 미존재). 9쪽 SVG 입수 시 동일 방식으로 교체하면 IM 전체 SVG화 완료

## 다음 단계
- IM 마크다운화 완료 — 추가 디자인/문구 다듬기는 사용자 지시별 진행
- DCM 덱도 동일 페이지 규칙 적용 검토(현재 미적용)
- 디자인 토큰/공통 규칙 변경은 theme/solaris.scss 한 곳만 수정 (두 덱 일괄 적용, 5·6쪽 도면 선택자 한정 주의)
- (검토) OneDrive 구버전 사본 정리 — 백업 가치 없음, 삭제 또는 `_OLD` 표식 권장
- WordPress Docs 메뉴에 IM/DCM URL 연결 확인

## 구조
- _quarto.yml — 사이트 설정 (랜딩 + 2개 덱)
- index.qmd — 랜딩(두 덱 진입 카드)
- im/index.qmd — INVESTMENT MEMORANDUM (560줄)
- dcm/index.qmd — Dynamic Collateral Management (158줄)
- theme/solaris.scss — 공용 디자인 토큰 (chain.link 톤)
- assets/ — 임베드 다이어그램
- .github/workflows/publish.yml — main push 시 자동 렌더·배포
