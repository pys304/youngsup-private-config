---
name: sop-frontmatter-plan
description: SOP 생성기/맵에 frontmatter·JSON·Markdown 4파일 출력과 버전 이력을 추가하기로 한 설계 결정
metadata: 
  node_type: memory
  type: project
  originSessionId: f32e0cf1-d2a4-4cff-a527-f8a5164de15f
---

SOP 도구(C:\Users\pys30\projects\06_자동화스크립트\ sop_generator.html / sop_map.html)에 2026-06-05 합의·**구현 완료**.

**구현 완료 (2026-06-05)**:
- 생성기: 완성본 저장이 4파일(Excel+PPT+Markdown+JSON) 동시 출력. buildMeta/saveJSON/saveMarkdown.
- 맵: JSON(meta+tasks)·MD(frontmatter+표) 불러오기, process_id 기반 업데이트 교체(분류·위치·연결 보존), predecessor/successor의 Process ID 기반 선·후행 자동연결(autoConnect). → 미해결이던 "업데이트 자동 불러오기" 숙제 해결됨.
- 남은 개선 여지: 생성기 단계에선 process_id/L1~L3/predecessor가 빈 값(맵에서 분류·연결 후 채워짐) → 맵에서 frontmatter 포함해 재export하는 흐름은 아직 없음. 필요 시 추가.

--- (이하 원래 설계 메모) ---

**배경**: 사내 피드백(설비기술담당)에서 "Excel·PPT 같은 그림이 아니라 JSON·Markdown 같은 데이터로도 저장하고, 모든 SOP에 정형화된 meta data(frontmatter)를 붙이면 AI가 먼저 읽고 상호 연결하기 좋다"는 제안을 받음.

**합의된 방향**:
- 결과물을 **4개 파일**로 출력: ① .xlsx(기존, 사람 보고용) ② .pptx(기존, 발표용) ③ .md(신규, frontmatter 포함 — 사람+AI용) ④ .json(신규, meta+tasks — 컴퓨터/Map용)
- ①②는 그대로 두고 ③④만 추가. frontmatter는 .md 파일 맨 앞에 포함(별도 파일 아님).
- 내부적으로 `buildMeta()` 공통 함수 하나로 frontmatter와 json의 meta를 동시 생성(값 어긋남 방지).
- 모든 값은 생성기가 이미 가진 데이터에서 자동 채움 — 추가 입력 없음.

**frontmatter 키**: process_id, process_name, version, company, team, assignee, L1/L2/L3, predecessor[], successor[], cycle, date, task_count, has_decision, systems[], departments[], improvement_count.

**버전 관리 = (B) 가벼운 이력 보관 방식으로 결정** (감사·점검 대응 위해). 최신본 1개만 유지하되 frontmatter에 history 줄(예: `- v2.0 (6/5) 승인 단계 추가`)만 누적. process_id는 고정 신분증 → Map이 같은 id 발견 시 "교체할까요?" 자동 인식 → 미해결 과제였던 [[업데이트 자동 불러오기]]와 연결.

**구현 순서 추천**: 단계1 생성기 JSON 저장(쉬움, 이미 JSON 보유) → 단계2 Markdown+frontmatter 저장 → 단계3 Map이 JSON·MD도 불러오기(predecessor/successor ID로 선·후행 자동 연결).
