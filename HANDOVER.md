# 뉴대한렌트카 마케팅 — 인수인계서 v3
> 최종 업데이트: 2026.04.27

---

## 🎯 프로젝트 목적 & 목표

- **회사**: 뉴대한렌트카 (제주 렌터카, 공항 8분 거리)
- **핵심 목표**: 플랫폼(제주페이 등) 의존도 낮추기 → 자사 홈페이지 직접 예약 전환율 향상
- **담당자**: Ran (마케팅 1인 운영, 임원 성과 보고 필요)
- **Claude 롤**: 마케팅 전문가 + 풀스택 개발자

---

## 🌐 배포 URL & 핵심 링크

| 용도 | URL |
|------|-----|
| 워크보드 | https://dhrent01-a.github.io/newdaehan-dashboard/workflow.html |
| 콘텐츠 대시보드 | https://dhrent01-a.github.io/newdaehan-dashboard/ |
| GitHub 저장소 | https://github.com/dhrent01-a/newdaehan-dashboard |
| Apps Script 웹앱 | https://script.google.com/macros/s/AKfycbxx8-Jg4T-REAH-wQrLvAWxQ96hnApPaqaAb3HzqrbZbC9abMmuo4tt9ljCqmIlvgMC/exec |
| 자사 홈페이지 | https://www.dhrent.co.kr |
| 예약 페이지 | https://www.dhrent.co.kr/tour.php?p=rent-list |
| 네이버 플레이스 | https://naver.me/5CWRQryf |
| 링크트리 | https://linktr.ee/dhrent |

---

## ✅ 완료된 작업 전체 이력

### 대시보드 (workflow.html + index.html)
- 탭 5개: ① 채널 운영 현황 / ② 월간 KPI / ③ 콘텐츠 스케줄 / ④ 분기 방향 / ⑤ URL 관리
- 오늘의 업무체크 — 클릭 순서 우선순위 숫자 표시 + 메모
- 월간 KPI — 채널 유입 집계 + 콘텐츠 성과 하이라이트 + 월간 종합
- 콘텐츠 스케줄 — 구글시트 읽기 전용
- URL 관리 — 구글시트 메타설정 탭 연동, 크로스 디바이스 공유
- ③ 탭명: 자사 전환율 추이 (읽기 전용, 워크플로우_KPI home 데이터 소스)
- loadDash() async 누락 오류 수정 완료
- KPI 전환율 % 형식 통일 완료

### Apps Script
- 구글시트 탭: 워크플로우_채널현황 / 워크플로우_KPI / 워크플로우_분기방향 / 콘텐츠스케줄 / 업무일지 / KPI성과기록 / 메타설정
- URL 크로스 디바이스 공유, 업무일지 날짜별 덮어쓰기, 분기방향 행 기준 덮어쓰기

### UTM 설정 (2026.04.27 확정)
- 전체 목적지: 메인페이지(`https://www.dhrent.co.kr/`) 로 통일 (기존 tour.php → 변경)
- 인스타그램 링크트리 적용 완료
- 카카오채널 AI자동응답 + 소식 링크 적용 완료
- 네이버 애널리틱스 설치 확인 → UTM 집계 환경 준비 완료

---

## 📊 UTM 링크 최종 확정본 (v3)

> ⚠️ 기존 v2 대비 변경: 목적지 전체 메인페이지로 변경

| 채널 | UTM 링크 |
|------|---------|
| 네이버 블로그 (신규 글 CTA) | `https://www.dhrent.co.kr/?utm_source=naver_blog&utm_medium=organic&utm_campaign=blog_cta` |
| 인스타그램 링크트리 예약 버튼 | `https://www.dhrent.co.kr/?utm_source=instagram&utm_medium=social&utm_campaign=profile_link` |
| 카카오채널 자동응답/소식/홈메인 | `https://www.dhrent.co.kr/?utm_source=kakao_channel&utm_medium=social&utm_campaign=channel_post` |
| 쓰레드 (재가입 후 적용 보관) | `https://www.dhrent.co.kr/?utm_source=threads&utm_medium=social&utm_campaign=threads_post` |
| 네이버 플레이스 | UTM 미적용 (네이버 구조상 불가, 유입상세URL에서 별도 확인) |

> Bitly 단축 적용 시: 단축 링크 → 원본 UTM으로 자동 리다이렉트 → 네이버 애널리틱스 집계 정상 작동

---

## 📅 블로그 UTM 교체 일정

- **대상**: 예약 발행 대기 115건 (기존 깨끗한 링크 → UTM 링크 교체)
- **방식**: 매월 첫째 주에 해당 월 + 다음 달 첫째 주 게시물 UTM 교체
- **발행 스케줄**: 주 3회, 26년 12월까지
- **데이터 수집 시작**: 2026년 5월부터 유효 데이터 집계 가능

---

## 🔑 채널별 KPI 집계 구조

| 채널 | 핵심 KPI | 측정 도구 |
|------|---------|---------|
| 네이버 블로그 | 월간 방문자 / 홈페이지 유입수 / 링크 클릭 | 네이버 애널리틱스 (UTM) |
| 인스타그램 | 프로필 방문 / 외부링크 클릭 / 링크트리→예약 클릭 | 인스타 인사이트 + 링크트리 통계 |
| 카카오채널 | 친구수 / 예약페이지 접근수 / 신규 친구 | 카카오 비즈니스 |
| 자사 홈페이지 | 플랫폼1위 예약수 / 자사 직접 예약수 / 자사 전환율% | 운영 시스템 수기 입력 |
| 네이버 플레이스 | 플레이스 유입 | 유입상세URL (m.place.naver.com) |
| 유튜브 | 추후 별도 논의 | — |

**자사 전환율 기준**: 자사 직접 예약 ÷ 총 예약(전체 채널 합산) × 100
> 총 예약은 운영 시스템에서 직접 확인 후 메모란에 `총예약건수: 000건 | 제주페이 000건` 형식으로 기록

**현재 자사 전환율 (2026.04)**: 695건(플랫폼) / 25건(자사) / 3.6%

---

## 📱 링크트리 구조 확정

| 순서 | 버튼 | 링크 |
|------|------|------|
| 1 | 🚗 실시간 렌트카 | UTM 인스타 링크 (적용 완료) |
| 2 | 💬 카카오톡 채팅 | 카카오채널 1:1 채팅 링크 |
| 3 | 📍 오시는 길 | https://naver.me/5CWRQryf |
| 4 | 📝 여행정보 & 후기모음 | 네이버 블로그 URL |

> 유튜브 링크트리 제외 확정 — 예약 전환 흐름 유지

---

## 🎬 다음 작업: 유튜브 콘텐츠 기획

- **5월 제주 출장 촬영 일정**: 2026.05.12 ~ 05.14
- 유튜브 콘텐츠 기획 및 제작 일정 픽스 필요
- OSMU 흐름: 유튜브 원본 → 인스타 릴스 재가공 → 인스타 내 설득 → 링크트리 → 예약

---

## 🔧 핵심 기술 맥락

- **저장 구조**: `saveAll()` → 채널현황+분기방향 / `saveKpiAll()` → KPI+하이라이트
- **URL 공유**: 구글시트 메타설정 탭 url_* 키로 저장 → 모든 기기 자동 로드
- **날짜 비교**: 구글시트 Date 객체 자동변환 → `instanceof Date` 체크 필수
- **DASH URL**: workflow.html 상단 `const DASH = 'https://script.google.com/...'`

### 과거 버그 & 해결 이력
| 버그 | 원인 | 해결 |
|------|------|------|
| CORS 오류 | `file://` 프로토콜 | GitHub Pages 호스팅 |
| `setHeader()` 비호환 | Apps Script TextOutput 미지원 | CORS 헬퍼 제거 |
| `deleteRows()` 범위 오류 | 범위 계산 오류 | `clearContents()` 로 전환 |
| 크로스 디바이스 동기화 실패 | localStorage 기반 URL 저장 | HTML에 URL 하드코딩 |
| 편집 버튼 scope 오류 | `btn.closest('td')` 버튼 이동 후 오작동 | `btn.closest('tr')` 로 변경 |

---

## 📁 새 채팅 첨부 파일 목록

```
workflow.html             ← 최신 outputs 버전
newdaehan_dashboard.html  ← 최신 outputs 버전
뉴대한렌트카_AppScript.gs  ← 최신 outputs 버전
HANDOVER.md               ← 본 파일
```

---

*새 채팅 첫 메시지 예시:*
> 뉴대한렌트카 마케팅 작업 이어서 진행합니다. HANDOVER.md + 파일 첨부 확인 후 다음 작업 시작해주세요.
