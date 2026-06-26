---
name: sop-preview-server
description: "SOP HTML 미리보기 서버 설정 — 포트 8766, 한글 경로 우회 래퍼 사용"
metadata: 
  node_type: memory
  type: project
  originSessionId: 3f61f070-c9c7-4d02-8b5c-17570900eaee
---

SOP HTML 미리보기는 `C:\Users\pys30\.claude\launch.json`의 **sop-preview** 설정(포트 8766) 사용. `python C:/Users/pys30/projects/.claude/serve_sop.py` 래퍼가 한글 폴더(06_자동화스크립트)로 chdir 후 서빙하며 루트는 generator로 리다이렉트.

**Why:** `http.server --directory`에 한글 경로를 직접 주면 무시되어 엉뚱한 폴더가 서빙됨. 또한 포트 8765는 기존 "계약서관리"(바탕화면 서빙) 설정이라 충돌 — 사용자가 404를 겪은 원인.

**How to apply:** preview_start는 "sop-preview"로 호출하고 URL은 `http://localhost:8766/sop_*.html` 사용. 수정 검증 시 캐시 회피를 위해 `?v=Date.now()` 쿼리 추가. 관련: [[sop-system-status]]
