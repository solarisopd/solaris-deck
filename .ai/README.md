# solaris-deck/.ai/ — 프로젝트 인수인계

SOLARIS OPPIDUM 발표 사이트 (Quarto + reveal.js).
CL-Link 투자설명자료(IM)와 동적담보관리(DCM) 두 슬라이드를 하나의 사이트로 묶어
GitHub Pages(public)로 배포 → WordPress Docs 메뉴에서 링크.

- 레포: https://github.com/solarisopd/solaris-deck.git (계정: solarisopd / 기본 브랜치: main)
- 집 PC: G:\solaris-deck
- 배포 URL: https://solarisopd.github.io/solaris-deck/ (랜딩) · /im/ · /dcm/

## 현재 상태 (2026-06-06)
- 마지막: 2026-06-06 / Claude Code / 집 PC
- IM 1쪽(표지)·2쪽(목차)을 slide_ai SVG로 교체 완료 (.svg-slide 방식, 아래 규약 참조)
- main 브랜치
- IM 덱 전면 재작성 완료 — 박세훈 ABL IM 원본 15쪽 + 확정 2쪽(자금순환·N:1) 삽입 (im/index.qmd 560줄)
- 목차 슬라이드 추가 + Pretendard 로컬 폰트 임베드
- 목차 페이지 raw HTML 렌더링 버그 수정
- GitHub Pages 빌드 실패 수정 (루트 index 폰트 경로)
- DCM 덱 7쪽 완성 (dcm/index.qmd 158줄)
- 주의: OneDrive `...\20260609PPT\solaris-deck\solaris-deck` 는 6/2 시점 비-Git 구버전 사본 → 작업 금지, 최신본은 G:\solaris-deck

## IM 슬라이드 SVG 교체 규약
- 원본: `C:\Users\MRB\OneDrive\00솔라리스오피둠\20260609PPT\slide_ai\NN.svg` (01~17, 파일번호 = 쪽번호)
- 교체 방식: SVG를 `im/slides/NN.svg`로 복사 → `im/index.qmd`에서 `![](slides/NN.svg){.slide-art}` 임베드
- 슬라이드 헤딩: `## &nbsp; {.svg-slide data-menu-title="..."}`. 어두운(네이비) 아트워크는 `background-color="#1A2A66"` 추가(여백 이음매 제거)
- **공통 유지(사용자 고정 지시)**: 하단 copyright `<div class="confidential">…</div>`는 각 슬라이드 유지 / 쪽번호(reveal `slide-number:c/t`)·넘김버튼(`controls`)은 전역 자동 적용 — 건드리지 말 것
- CSS: theme/solaris.scss `.reveal section.svg-slide`(img.slide-art = absolute/inset:0/object-fit:contain) / frontmatter `auto-stretch:false` 필수(미설정 시 r-stretch가 풀블리드 깨뜨림)
- 진행: 2026-06-06 1쪽(표지)·2쪽(목차) 완료. 3~17쪽은 SVG 첨부 시 동일 방식

## 다음 단계
- IM 3~17쪽 SVG 교체 (사용자 SVG 첨부 시 위 규약대로)
- (검토) OneDrive 구버전 사본 정리 — 백업 가치 없음, 삭제 또는 `_OLD` 표식 권장
- assets/ Octopus N:1 다이어그램(slide3.html) 추가 후 IM 임베드 검토
- 디자인 토큰 변경은 theme/solaris.scss 한 곳만 수정 (두 덱 일괄 적용)
- WordPress Docs 메뉴에 IM/DCM URL 연결 확인

## 구조
- _quarto.yml — 사이트 설정 (랜딩 + 2개 덱)
- index.qmd — 랜딩(두 덱 진입 카드)
- im/index.qmd — INVESTMENT MEMORANDUM (560줄)
- dcm/index.qmd — Dynamic Collateral Management (158줄)
- theme/solaris.scss — 공용 디자인 토큰 (chain.link 톤)
- assets/ — 임베드 다이어그램
- .github/workflows/publish.yml — main push 시 자동 렌더·배포
