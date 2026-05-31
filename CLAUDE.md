# ttobe.github.io — 황진혁 백엔드 개발자 포트폴리오

개인 포트폴리오 + PDF 이력서를 겸하는 단일 정적 사이트. GitHub Pages(`https://ttobe.github.io/`)로 배포된다.

## 핵심 원칙 (반드시 지킬 것)

1. **내용은 실제 정보만.** 수치·경력·기술스택을 절대 지어내지 않는다. 새 사례/지표를 넣을 땐 사용자에게 실제 값을 확인한다. (과거 Claude Design이 생성한 `portfolio/data.js`에는 가짜 회사·수치·학력이 들어 있었음 — 참고만 하고 내용 출처로 쓰지 말 것.)
2. **정적 단일 파일 구조.** 내용·구조는 `index.html`에 인라인, 스타일은 `style.css`. JS 렌더링/빌드 단계 없음 (JS 없이도 보여야 하고, PDF·검색·링크 미리보기에 유리). 작은 향상(nav 활성 하이라이트)만 인라인 `<script>`로.
3. **화면과 인쇄(PDF)를 함께 고려.** 모든 디자인 변경은 `@media print`에서 깨지지 않는지 확인한다(그림자·배경·애니메이션 제거, 코드블록 라이트 전환, 페이지 브레이크 유지).
4. **커밋 계정.** author/committer는 **`ttobe <ahdrmfgur12@naver.com>`** (개인 GitHub 계정). 회사 이메일 `hwang.jinhyuk@cashwalk.io`(=backend-jinhyuk 계정)로 커밋하지 말 것. 레포 로컬 git config에 이미 올바르게 설정돼 있으니 `-c user.email=...`로 덮어쓰지 않는다.
5. **보안·정책 민감 내용 비노출.** 특히 어뷰징 대응처럼 회피에 악용될 수 있는 내용은 구체적 **탐지 신호·기준·임계값**(예: "초대 관계로 묶음", "이메일 검증", 클러스터 크기 "20", "매 1시간" 주기), **내부 팀 코드네임**(예: "AP랩"), **외부 벤더명**(예: ZeroBounce)을 쓰지 않고 일반화한다(예: "계정 간 관계", "외부 API", "일정 규모 이상", "주기적"). 차단 규모 같은 사업 수치도 노출 범위를 사용자와 확인한다. 민감 내용이 들어갔다 빠지면 **git 히스토리에도 남지 않게** 정리한다(필요 시 단일 커밋 스쿼시 후 force-push).

## 파일 구성

```
index.html      배포되는 페이지 (내용 + 구조 인라인)
style.css       전체 스타일 (① 미니멀 라이트 테마 기반)
favicon.svg     accent 블루 라운드 사각형 + "황"
포트폴리오_황진혁.pdf   배포용 PDF (아래 명령으로 재생성)
portfolio/, screens/   Claude Design 원본 시안(다크/매거진 포함) + 미리보기 — .gitignore 처리, 로컬 참고용. data.js 내용은 가짜이므로 신뢰 금지
```

## 디자인 기준 (① 미니멀 라이트)

Claude Design에서 받은 3개 시안 중 **1번 "미니멀 라이트"** 방향을 채택. 출처: `portfolio/base.css` + `portfolio/theme-light.css` + `portfolio/render.js`.

- **폰트**: 본문 `Noto Sans KR`, 라벨·숫자·코드·메타 `JetBrains Mono` (Google Fonts, `<head>`에서 로드)
- **포인트 컬러(accent)**: `#2f54eb` (CSS 변수 `--accent`)
- **레이아웃**: 880px 단일 컬럼(`--maxw`), `#eceef2` 캔버스 위에 흰 문서 시트
- **분위기**: 넉넉한 여백, 가는 1px 선, 절제된 블루 포인트. 메트릭 카드의 큰 파란 숫자는 **실제 수치가 없어 사용하지 않고**, 대신 실제 성과는 콜아웃(`.pf-callout`)으로 표현
- **주요 컴포넌트 클래스**: `.pf-header` / `.pf-section`+`.pf-section-head`(`01 경력 Career`) / `.pf-job`(경력, 좌측 기간·우측 본문) / `.pf-roles`(타임라인) / `.pf-duty` / `.pf-case`+`.pf-case-block`(좌측 88px 라벨 그리드) / `.pf-table`(`.hl`로 핵심 셀 강조) / `.pf-code`(다크 코드블록) / `.pf-callout`(성과) / `.pf-review`("후기 —") / `.pf-proj-block`(프로젝트별 메타 + 서브케이스 1-1~3-1) / `.pf-mini-list`(경험·학력)
- 긴 소제목(예: "의사결정 1 · …")은 좌측 라벨을 짧게(`의사결정 1`) 두고, 상세는 본문 첫 줄 `.pf-lead`(굵게)로 처리해 88px 라벨 컬럼이 깨지지 않게 한다.

## 콘텐츠 구조

`01 경력`(넛지헬스케어, 2025.05~, 파트장/개발자 2역할 + 업무) → `02 주요 업무`(CASE 01 Nginx 499 / 02 GA4 DAU / 03 어뷰징 클러스터링 Union-Find / 04 업무 요청 방식 개선 / 05 청자 맞춤 커뮤니케이션·velog / 06 오퍼월 광고 연동·velog) → `03 프로젝트`(fancamp 1-1~1-4 / kopilot 2-1~2-2 / ME:RROR 3-1) → `04 경험·학력`(부스트캠프·KT Aivle·생명정보학 연구생 / 홍익대). velog 글은 별도 섹션이 아니라 주요 업무의 CASE로 편입(CASE-no에 "· 주간 리포트 #N", 본문에 velog 링크).

## PDF 재생성

`index.html`/`style.css`를 바꾸면 배포용 PDF도 다시 뽑아야 한다(웹 변경이 자동 반영되지 않음). 헤드리스 Chrome 사용:

```bash
CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
"$CHROME" --headless=new --disable-gpu --no-pdf-header-footer \
  --print-to-pdf="포트폴리오_황진혁.pdf" --virtual-time-budget=4000 \
  "file://$PWD/index.html"
```

- 변경 검증용 스크린샷도 같은 방식(`--screenshot=...`, `_shot/`은 gitignore)으로 확인. 페이지 확인은 PDF를 직접 페이지 단위로 열어본다.

### PDF 페이지네이션 규칙 (`@media print`)

목표: **요소가 페이지 중간에서 어색하게 잘리지 않게**, 그리고 **들어갈 수 있으면 한 페이지에 여러 케이스를 채운다**(빈 공간 최소화). 모든 규칙은 `style.css`의 `@media print` 안에 있다.

- **여백·밀도**: `@page { margin: 12mm }`. 인쇄 전용으로 본문/표/코드/메트릭 글자·줄간격·여백을 화면보다 줄여 케이스가 한 페이지에 들어가도록 압축한다(본문 `~11.5px`, line-height `1.4~1.45`). 내용이 늘면 이 값들을 더 조여 페이지 수를 억제한다.
- **섹션 분리**: `#experience`만 `break-before: page`로 새 페이지 시작(경험·학력이 프로젝트와 안 섞이게). 나머지 섹션(경력·주요 업무·프로젝트)은 강제 분할하지 않고 자연스럽게 흐르며 패킹한다.
- **제목 보호**: `.pf-section-head`, `.pf-case-head`, `.pf-proj-bar`, `.pf-projmeta`, 프로젝트 `.pf-tags`에 `break-after: avoid` → 섹션/케이스 제목·프로젝트 인트로(이름·메타·태그)가 본문/첫 서브케이스와 분리돼 페이지 끝에 혼자 남지 않는다.
- **통째 유지 시도**: `.pf-case`, `.pf-job`, `.pf-extra`, `.pf-extra-col`에 `break-inside: avoid` → 들어가면 통째로, 넘치면 아래 단위에서만 분할.
- **절대 안 잘리는 단위**: `.pf-case-block`(문단 묶음), `.pf-table`, `.pf-code`, `.pf-callout`, `.pf-metrics`/`.pf-metric`, `.pf-review`, `.pf-mini-row`, `.pf-duty`에 `break-inside: avoid` → 문단·표·코드·카드 중간이 절대 잘리지 않는다.
- **트레이드오프**: 통째 유지 때문에 다음 케이스가 안 들어가면 페이지 하단에 여백이 생길 수 있다(중간 잘림보다 이쪽을 택함). 검증은 PDF를 페이지별로 열어 ① 제목만 남은 페이지 없는지 ② 문단·표 중간 잘림 없는지 ③ 들어갈 수 있는데 다음 장으로 밀린 케이스 없는지 본다.

## 배포 / 검증

- `master`에 push하면 GitHub Pages가 재빌드 → 1~2분 후 라이브.
- 라이브 확인: `https://ttobe.github.io/` (favicon·CSS는 브라우저 캐시 때문에 강력 새로고침 필요할 수 있음).
