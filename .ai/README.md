# solaris-deck/.ai/ — 프로젝트 인수인계

SOLARIS OPPIDUM 발표 사이트 (Quarto + reveal.js).
CL-Link 투자설명자료(IM)와 동적담보관리(DCM) 두 슬라이드를 하나의 사이트로 묶어
GitHub Pages(public)로 배포 → WordPress Docs 메뉴에서 링크.

- 레포: https://github.com/solarisopd/solaris-deck.git (계정: solarisopd / 기본 브랜치: main)
- 집 PC: G:\solaris-deck
- 배포 URL: https://solarisopd.github.io/solaris-deck/ (랜딩) · /im/ · /dcm/

## 현재 상태 (2026-06-06)
- 마지막: 2026-06-06 / Claude Code / 집 PC
- main 브랜치, origin과 완전 동기화(0/0), working tree clean
- IM 덱 전면 재작성 완료 — 박세훈 ABL IM 원본 15쪽 + 확정 2쪽(자금순환·N:1) 삽입 (im/index.qmd 560줄)
- 목차 슬라이드 추가 + Pretendard 로컬 폰트 임베드
- 목차 페이지 raw HTML 렌더링 버그 수정
- GitHub Pages 빌드 실패 수정 (루트 index 폰트 경로)
- DCM 덱 7쪽 완성 (dcm/index.qmd 158줄)
- 주의: OneDrive `...\20260609PPT\solaris-deck\solaris-deck` 는 6/2 시점 비-Git 구버전 사본 → 작업 금지, 최신본은 G:\solaris-deck

## 다음 단계
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
