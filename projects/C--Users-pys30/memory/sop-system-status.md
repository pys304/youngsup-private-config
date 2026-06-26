---
name: sop-system-status
description: SOP 3단계 시스템(generator/map/graph) 기능 현황 및 작업 관례 (2026-06-12 기준)
metadata: 
  node_type: memory
  type: project
  originSessionId: 3f61f070-c9c7-4d02-8b5c-17570900eaee
---

SOP 시스템 (C:\Users\pys30\projects\06_자동화스크립트, GitHub pys304/projects master) 주요 현황:

- **주목적: End to End Process 발굴** — graph는 E2E 체인 추적(노드 클릭 시 사슬 전체 강조), DAG(흐름) 레이아웃, E2E 워딩 적용됨
- graph: 예시 불러오기/비우기 (map과 동일 108개 L4 샘플, 연결 66건), 레이아웃 3종(Force/L1 군집/흐름)
- map: 연결 추천 기능(휴리스틱: 산출물↔투입물·키워드·단계어 + A.biz 프롬프트 경로), autoConnect 이름 매칭 fallback, dirty 감지 전 경로 보완(beforeunload 경고 포함)
- generator: ? 버튼 호버 툴팁, 로고 헤더 우측 고정

**Why:** 사용자가 기능 추가 시 "검토→추천→구현" 흐름을 선호하며, 매번 VDI 번들→commit→push→VDI 파일 전달까지 요구함.

**How to apply:** 수정 후 반드시 ① node --check로 스크립트 문법 검사(과거 변수 충돌 사고), ② 미리보기(launch 설정 sop-preview, 포트 8766, [[sop-preview-server]])에서 기능 검증, ③ `$env:PYTHONIOENCODING='utf-8'; python bundle_for_vdi.py`, ④ commit+push, ⑤ SendUserFile로 _vdi.html 전달.
