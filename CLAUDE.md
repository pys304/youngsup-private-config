# Claude 글로벌 설정

## 사용자 정보
- 소속 회사: SK에코플랜트 머티리얼즈
- 반도체 소재 제조업종 근무
- 기업문화담당 / Infra협력팀 팀장
- 담당 업무: 총무, 대관, 홍보, 산업단지, HR 연관 업무

## 답변 방식
- 결론을 항상 맨 위에 불릿포인트로 먼저 제시
- 이후 친절하고 자세하게 설명
- 기본 언어: 한국어 (영어 단어 포함 가능)
- 할루시네이션 금지: 확실하지 않으면 모른다고 말할 것
- 핵심만 간결하게, 불필요한 내용 제거
- 토큰 절약: 불필요한 반복, 과도한 설명 금지
- 서브태스크 폴링 최소화: 직접 처리 가능한 작업은 태스크 분리 없이 처리, 폴링은 2~3회 이내

## 결과물 방식
- 코드는 복사해서 바로 쓸 수 있는 완성본으로 제공
- 코드 주석은 한국어로 작성
- 디자인 시: 아래 [디자인 시스템] 섹션의 규칙을 항상 적용
- 모든 결과물은 누르면 바로 실행·열람 가능한 파일 형태로 제공 (HTML, Python 스크립트 등 실행 파일로 첨부)

## 주요 작업 유형
- HTML 페이지 (사내 공지, 홍보물 등)
- Markdown 문서
- Python 스크립트 (업무 자동화)
- 이미지 홍보물 관련 코드

## 환경
- 결과물은 사내 VDI망으로 옮겨 사용
- 외부 API, 클라우드 연동 최소화
- 외부 의존성 없이 단독 실행 가능한 형태 선호

---

## 디자인 시스템 (SK에코플랜트 머티리얼즈)

> 모든 결과물(HTML, Python GUI, 슬라이드, 문서 등)에 아래 디자인 규칙을 기본 적용한다.

### 디자인 토큰 — 색상

**브랜드 4색 팔레트:**
```css
--brand-black:    #0A0F14;  /* 헤딩, 다크 배경, 기본 버튼 */
--brand-darkgray: #2E3640;  /* 중간 톤, 푸터 */
--brand-red:      #EA002C;  /* 주 액센트, CTA, 활성 상태 */
--brand-orange:   #FF7A00;  /* 보조 액센트 */
```

**중립 색상:**
```css
--gray-100: #F4F6F8;
--gray-200: #E5E9EE;
--gray-400: #9BA5B0;
--gray-500: #6B7682;
--fg-1:     var(--gray-900);
--fg-2:     var(--gray-700);
--fg-3:     var(--gray-500);
--border-1: var(--gray-200);
```

- 색상 선택은 작은 액센트 목적으로만 제한
- 빨강·오렌지는 대형 배경으로 사용 금지

### 타이포그래피

**폰트 패밀리:**
```css
--font-body:       'IBM Plex Sans KR', sans-serif;  /* 한글 본문 */
--font-display:    'IBM Plex Sans KR', sans-serif;  /* 헤딩, 디스플레이 */
--font-en:         'Source Sans 3', sans-serif;     /* 영문, eyebrow */
--font-kr-display: 'Gowun Dodum', sans-serif;       /* 브랜드 강조 */
```

**타입 스케일:**
```css
--fs-hero:    clamp(48px, 6.5vw, 96px);
--fs-display: clamp(36px, 4.5vw, 64px);
--fs-h1:      clamp(32px, 3.2vw, 48px);
--fs-h2:      clamp(26px, 2.4vw, 36px);
--fs-h3:      22px;
--fs-body:    16px;
--fs-sm:      14px;
--fs-eyebrow: 12px;  /* letter-spacing: 0.16em, uppercase */
```

**폰트 웨이트:**
- 헤딩: 800, letter-spacing: -0.035em
- 히어로: 800, letter-spacing: -0.045em
- 본문: 400–500

### 레이아웃

```css
/* 기본 컨테이너 */
max-width: 1280px;
margin: 0 auto;
padding: 0 40px;

/* 섹션 간격 */
padding: 128px 0;

/* 헤더 */
height: 72px;
position: sticky;
backdrop-filter: blur(20px);
```

- 카드 그리드: 3컬럼 gap 12px (사업 카드), 4컬럼 (자회사 탭)

### 컴포넌트 규칙

**버튼 (SKButton):**
```
variant: 'primary' | 'secondary' | 'ghost' | 'onDarkSolid' | 'onDark'
size:    'sm' | 'md' | 'lg'
border-radius: 999px  /* pill 형태 */
```

**섹션 라벨 (SKEyebrow):**
- 항상 영문 대문자, letter-spacing: 0.16em
- 왼쪽에 빨강 22px 짧은 선 자동 추가
- tone: "light" 또는 "dark"

**섹션 타이틀 (SKSectionTitle):**
- eyebrow, title, subtitle, tone 속성 지원

**컨테이너 (SKContainer):**
- maxWidth: 1280px, margin: 0 auto, padding: 0 40px

### 카드 디자인 규칙

```css
background:    #ffffff;
border:        1px solid var(--border-1);
border-radius: 8px 또는 16px;
box-shadow:    var(--shadow-sm);

/* 상단 액센트 선 */
width: 22px; height: 2px; background: var(--brand-red);

/* 호버 */
border-color: var(--brand-black);
transform: translateY(-4px);
box-shadow: var(--shadow-md);
```

### 다크 섹션 (Hero, Sustainability, Footer)

```css
background:   var(--brand-black);   /* #0A0F14 */
color:        var(--gray-300);
/* 메타 텍스트 */
color:        var(--gray-400);

/* 다크 카드 */
background:   rgba(255, 255, 255, 0.04);
border:       1px solid rgba(255, 255, 255, 0.08);
```

- 글로우·그라디언트 패턴 사용 금지

### 카피라이팅 규칙

- 한국어: 격식체 (~합니다, ~습니다)
- CTA 문구: "더 보기", "자세히 보기", "살펴보기"
- 금지 문구: "시작하기", "지금 바로"
- 이모지, 느낌표 절대 사용 금지
- 영문 대문자 사용: 섹션 라벨, 네비게이션, 약어 (ESG, OLED, VWBE)

### 금지 사항

| 금지 항목 | 대체 방법 |
|---|---|
| `#000000` 순수 검정 | `var(--brand-black)` 사용 |
| 빨강·오렌지 대형 배경 | 작은 액센트 목적으로만 |
| 좌측 보더 스트라이프 카드 | 상단 22px 액센트 선 사용 |
| 글래스모피즘, 뉴모피즘 | 플랫 + 미니멀 카드 |
| 이모지 아이콘 카드 | 텍스트·SVG 아이콘 |
| 블루-퍼플 그라디언트 | 브랜드 4색 팔레트 준수 |
| Tailwind CSS | 인라인 스타일 + CSS 변수 |

---

## 설치된 플러그인 (anthropics/knowledge-work-plugins)

> Claude Code 터미널에서 `claude` 실행 후 슬래시 명령으로 호출한다.
> 사용법: `/플러그인명:작업내용`

### 플러그인 자동 실행 규칙
- 단순 질문·대화 → 플러그인 없이 바로 답변
- 문서·양식·보고서·체크리스트·공지문 등 결과물 생성 시 → 아래 표에서 해당 플러그인 자동 실행

| 플러그인 | 슬래시 명령 | 주요 활용 업무 |
|---|---|---|
| human-resources | `/human-resources:` | 온보딩 자료, 인사규정, 평가 양식, 교육 자료 |
| legal | `/legal:` | 계약서 검토, 법령 검토, 인허가 문서, 대관 업무 |
| marketing | `/marketing:` | 사내 공지, 홍보물, SNS 콘텐츠, 뉴스레터, 사보 |
| operations | `/operations:` | 총무 체크리스트, 시설·비품·차량 관리 |
| productivity | `/productivity:` | 일정 관리, 업무 계획, 회의록, 주간보고 |
| pdf-viewer | `/pdf-viewer:` | PDF 문서 열람 및 내용 분석 |
| enterprise-search | `/enterprise-search:` | 사내 문서·파일 검색 |

### 플러그인 사용 예시
```
/human-resources:신입직원 온보딩 체크리스트 만들어줘
/legal:이 계약서에서 불리한 조항 찾아줘
/marketing:6월 사내 행사 공지문 초안 작성해줘
/operations:비품 재고 관리 양식 만들어줘
/productivity:이번 주 업무 계획표 만들어줘
```
