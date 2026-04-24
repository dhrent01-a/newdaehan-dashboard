# 뉴대한렌트카 마케팅 — 채팅 인수인계서

> 최종 업데이트: 2026-04

---

## 🎯 프로젝트 목적

**회사:** 뉴대한렌트카 (제주 렌터카, 공항 8분 거리)  
**핵심 목표:** 플랫폼(KakaoT 등) 의존도 낮추기 → 자사 홈페이지 직접 예약 전환율 향상  
**담당자:** Ran (마케팅 1인 운영)

---

## 🌐 배포 URL

| 용도 | URL |
|------|-----|
| 콘텐츠 대시보드 (index) | `https://dhrent01-a.github.io/newdaehan-dashboard/` |
| 마케팅 워크보드 | `https://dhrent01-a.github.io/newdaehan-dashboard/workflow.html` |
| GitHub 저장소 | `https://github.com/dhrent01-a/newdaehan-dashboard` |
| Apps Script 웹앱 | `https://script.google.com/macros/s/AKfycbxx8-Jg4T-REAH-wQrLvAWxQ96hnApPaqaAb3HzqrbZbC9abMmuo4tt9ljCqmIlvgMC/exec` |

---

## 🤖 Claude 역할

마케팅 전문가 + 풀스택 개발자. 전략 자문 + 코드 수정 동시 수행.  
**브라우저 연결 시도 금지** — 코드 분석 + 파일 수정으로만 작업.  
**긴 요청 시 작업 방향 브리핑 후 확인 단계 거쳐서 수행.**

---

## 📁 관리 파일 (3개)

| 파일 | 용도 |
|------|------|
| `workflow.html` | 마케팅 워크보드 (개인 업무용) |
| `newdaehan_dashboard.html` → `index.html` | 콘텐츠 대시보드 (임원 공유용) |
| `뉴대한렌트카_AppScript.gs` | Google Apps Script 백엔드 |

---

## ✅ 현재 완료 상태

### workflow.html (마케팅 워크보드)

탭 구성 5개:
- ① 채널 운영 현황 — 채널별 체크리스트 + 자사 예약 전환 현황 박스 (loadDash 연동)
- ② 월간 KPI — 채널 유입 집계 + 콘텐츠 성과 하이라이트 + 월간 종합 (구글시트 저장)
- ③ 콘텐츠 스케줄 — 구글시트 읽기 전용
- ④ 분기 방향 — 구글시트 저장/불러오기
- ⑤ URL 관리 — 구글시트 메타설정 탭 연동 (크로스 디바이스)

주요 기능:
- 업무일지 날짜별 저장 (`업무일지` 탭, Date 객체 처리 포함)
- KPI 성과 하이라이트 제목 기준 덮어쓰기 (`KPI성과기록` 탭)
- 오늘의 업무체크 클릭 순서 우선순위 숫자 표시
- KPI/분기 데이터 — 구글시트 캐시(`_gsKpi`, `_gsQuarter`) 기반으로 모바일 크로스 디바이스 정상 작동

### newdaehan_dashboard.html (콘텐츠 대시보드)

탭 구성 5개:
- ① OSMU 콘텐츠 현황
- ② Trip Plan
- ③ 자사 전환율 추이 — 읽기 전용, `워크플로우_KPI` home 데이터 기반 바 차트
- ④ 공지 동기화
- ⑤ 채널 URL 관리 — 구글시트 자동 동기화

③ 자사 전환율 추이 상세:
- 지표 계산: **자사 직접 예약 ÷ 1위 플랫폼 예약 × 100** (전체 예약 대비 아님)
- 목표 전환율 입력칸 — 기본값 10%, 변경 시 달성률 바 즉시 반영, 구글시트 `메타설정` 탭 `url_conv_goal` 키로 저장
- 목표선 그래프 없음 (스케일 문제로 제거, 달성률 바로 대체)

### Apps Script (뉴대한렌트카_AppScript.gs)

구글시트 탭 구성:

| 탭명 | 용도 |
|------|------|
| `예약전환율` | 대시보드 예약 데이터 |
| `OSMU콘텐츠` | 콘텐츠 현황 |
| `공지동기화` | 공지 동기화 로그 |
| `메타설정` | URL 크로스 디바이스 공유 (`url_*` 키), 목표 전환율 (`url_conv_goal`) |
| `워크플로우_채널현황` | 워크보드 채널 상태 |
| `워크플로우_KPI` | KPI 데이터 (ch 필드로 채널 구분, home 포함) / v3(전환율) % 형식 저장 권장 |
| `콘텐츠스케줄` | 콘텐츠 일정 |
| `워크플로우_분기방향` | 분기별 전략 메모 |
| `업무일지` | 날짜별 업무 기록 |
| `KPI성과기록` | 성과 하이라이트 (제목 기준 덮어쓰기) |

API 액션:
- `?action=load` → 대시보드 데이터 (booking / osmu / syncLog / meta)
- `?action=loadWf` → 워크보드 데이터 (ch / kpi / sched / quarter / urls)

---

## 🔧 핵심 기술 맥락

### 저장 구조
- `saveAll()` → 채널현황 + 분기방향
- `saveKpiAll()` → KPI + 성과 하이라이트
- `saveToSheet()` → 채널현황만

### 크로스 디바이스 구조
- KPI/분기: `loadFromSheet()` 호출 시 `_gsKpi`, `_gsQuarter` 메모리 캐시 저장 → 월/분기 셀렉터 변경 시 캐시 우선 읽기 → localStorage는 같은 기기 fallback
- URL: 구글시트 `메타설정` 탭 `url_*` 키로 저장
- `loadFromSheet()`는 `setTimeout(..., 100)`으로 지연 호출 (셀렉터 세팅 완료 후 실행 보장)

### 주의 사항
- **날짜 비교:** 구글시트가 날짜를 Date 객체로 자동변환 → `instanceof Date` 체크 필수
- **DASH URL:** `workflow.html` 상단 `const DASH = '...'` 하드코딩
- **APPS_SCRIPT_URL:** `newdaehan_dashboard.html` 상단 `const APPS_SCRIPT_URL = '...'` 하드코딩
- **CORS:** Apps Script는 CORS 자동 허용 — `setHeader()` 사용 금지 (TextOutput 미지원)
- **삭제:** `deleteRows()` 대신 `clearContents()` 사용
- **KPI v3 형식:** 코드에서 `rate < 1 ? rate*100 : rate` 로 소수/% 양쪽 처리 중. 구글시트에서 % 형식으로 통일 권장

### 과거 해결된 버그 (재발 방지)

| 증상 | 원인 | 해결 |
|------|------|------|
| CORS 오류 | `file://` 프로토콜 | GitHub Pages 호스팅 |
| `setHeader()` 오류 | TextOutput 미지원 | CORS 헬퍼 제거 |
| `deleteRows()` 범위 오류 | 범위 계산 문제 | `clearContents()` 교체 |
| 크로스 디바이스 URL sync 실패 | localStorage 기반 저장 | HTML에 URL 하드코딩 |
| Edit 버튼 scope 오류 | `btn.closest('td')` 이동 후 깨짐 | `btn.closest('tr')` 변경 |
| loadDash 파싱 오류 | `async` 3중 중복 | `async function loadDash()` 수정 |
| 모바일 KPI/분기 데이터 0 표시 | `loadKpi()`/`loadQ()`가 localStorage만 읽음 | 구글시트 캐시(`_gsKpi`, `_gsQuarter`) 구조로 변경 |
| 목표선 바닥에 붙는 문제 | 플랫폼 예약 스케일 대비 자사 예약 너무 작음 | 목표선 제거, 달성률 바로 대체 |

---

## 📋 새 채팅 시작 시 첨부 파일

```
workflow.html
newdaehan_dashboard.html
뉴대한렌트카_AppScript.gs
HANDOVER.md
```
