# 🧭 AI & Tech Study Hub — 복원용 Setup 파일
> 이 문서는 Notion, GitHub, SQLD 연동 프로젝트의 전체 구조와 상태를 복원하기 위한 설정 파일입니다.  
> 새 ChatGPT 세션에서 이 파일을 업로드하면 이전 진행 상태를 완전히 이어서 복구할 수 있습니다.

---

## 🧩 전체 시스템 개요

### 🧱 구성 요소
| 구성 | 설명 |
|------|------|
| 📘 **AI & Tech Study Hub** | 메인 허브 페이지 (전체 공부 관리 중심) |
| 📈 **Growth Log** | Hub 내부의 “학습 기록용 표 보기 데이터베이스” |
| 🎓 **Certifications** | 자격증 관련 공부 모음 페이지 |
| 🟦 **SQLD Study Dashboard** | SQLD 자격증 준비용 서브 대시보드 페이지 |
| 🐙 **GitHub Study-Log** | 학습 결과를 Markdown으로 버전 관리하는 저장소 |

---

## 🗂️ Notion 구조 (확정 버전)

📘 **AI & Tech Study Hub**
 ┣ 📈 Growth Log
 ┗ 🎓 Certifications
     ┗ 🟦 SQLD Study Dashboard
         ├─ SQLD 자격증 준비 일정
         ├─ 이론 / 기출 / 최종 정리 단계
         └─ Notion → GitHub 연계 학습 기록

### 📘 AI & Tech Study Hub 설정 요약
- **Growth Log**: 표 보기 DB로 매일의 학습 기록 관리  
- **Certifications**: SQLD, 정보처리기사, Network 등 하위 페이지 관리  
- **상단 섹션**: callout 블록에 위 구조 다이어그램 삽입  

---

## 🧾 SQLD_Study_Dashboard.md (현재 GitHub 등록본)

- 위치: `Study-Log/SQLD/SQLD_Study_Dashboard.md`
- 커밋 메시지:
  ```
  chore(log): add SQLD Day 01 – 모델링 복습 (2025-10-13, KST)
  ```
- GitHub Repository: `https://github.com/Raprok612/Study-Log`
- Notion 연결 위치: `🎓 Certifications` → `🟦 SQLD Study Dashboard`

---

## 🌍 시간대 / 커밋 기준

| 기준 | 지역 | 설명 |
|------|------|------|
| 현지 개발 시간 | 🇹🇭 태국 (UTC+7) | 실시간 커밋 기준 |
| GitHub 히트맵 | UTC | 커밋 일자 계산 |
| 목표 | 한국 기준 하루 1커밋 유지 (UTC+9 반영 시 약 2시간 오차) |

---

## 💡 추천 작업 순서

1️⃣ **Notion 연결**
   - SQLD Study Dashboard 페이지에 “📈 Growth Log 바로가기” 링크 추가  
   - AI & Tech Study Hub 상단에 다이어그램(callout) 블록 삽입  

2️⃣ **GitHub 관리**
   ```bash
   cd ~/projects/Study-Log
   git add .
   git commit -m "chore(log): update SQLD Day 02 progress (YYYY-MM-DD, KST)"
   git push
   ```

3️⃣ **Notion ↔ GitHub 주기적 백업**
   - Notion 페이지 Export → Markdown  
   - Study-Log 리포지토리의 동일 폴더(`SQLD/`)에 업로드  
   - 주 1회 커밋으로 유지  

---

## ⚙️ 자동화 / 향후 확장 계획

| 항목 | 설명 |
|------|------|
| 🔁 Notion → GitHub 자동 백업 | weekly-log.yml (GitHub Actions)로 주간 자동 푸시 |
| 🧠 Growth Log 자동 템플릿 | Day N 자동 생성 및 날짜 삽입 |
| 🧩 SQLD 외 확장 | InfoProc, Network, Bootcamp 학습 페이지 추가 예정 |

---

## 🧱 복원 지침 (새 채팅 시작 시)
새 채팅에서 아래 한 줄 입력 후 이 파일을 업로드하세요 👇

```
어제의 AI & Tech Study Hub setup 파일 기준으로 이어서 하자.
```

이후 ChatGPT가 자동으로:
- SQLD / Growth Log / Notion / GitHub 구조를 인식하고
- 이전에 진행하던 연결 및 자동화 단계부터 재개합니다 ✅

---

🗓️ **마지막 업데이트:** 2025-10-13  
✍️ **작성자:** Jaerok Kim (Raprok612)
