# 🧭 AI & Tech Study Hub Setup (2025)
> 📚 SQLD / Growth Log / Certification 통합 관리 및 Git ↔ Notion 연동 규칙서  
> 작성자: Jaerok Kim (Raprok612)  
> 최신 업데이트: 2025-10-18

---

## 📂 Notion Page Structure

📘 **AI & Tech Study Hub**  
│  
├── 📈 **Growth Log**  
│        └─ 학습 일지, SQLD / AI / MLOps 진척 관리 (표 보기 데이터베이스)  
│  
└── 🎓 **Certifications**  
    └── 🟦 **SQLD Study Dashboard**  
         ├─ SQLD 자격증 준비 일정 (10.13 ~ 11.16)  
         ├─ 이론 / 기출 / 최종 정리 단계 구분  
         ├─ `sqld/notes/` 기반 Git ↔ Notion 연동  
         └─ 시험 전 최종 암기/오답 복습 관리

> 💡 Notion의 **AI & Tech Study Hub**는 Git의 `study-log` 폴더 구조와 완전히 일치하도록 설계되어 있습니다.

---

## 📂 1. 폴더 구조
```
projects/
└── study-log/
    ├── sqld/                       # SQLD 학습
    │   ├── notes/                  # Day별 학습 노트 (Notion ↔ Git 연동)
    │   ├── reference/              # 요약노트 / 참고자료
    │   └── growth_log/             # 학습 인덱스 (Notion Growth Log 대응)
    └── AI_Tech_Study_Hub_setup.md  # 이 문서
```

---

## 🧩 2. 파일 작성 규칙

### 🗓️ Day별 노트
- 파일명: `dayNN_주제명.md`
- 제목: `# SQLD Day NN – 주제명 (YYYY-MM-DD)`
- 커밋 메시지:  
  `chore(log): add SQLD Day NN – 주제명 (YYYY-MM-DD)`

### 📈 Growth Log
- 파일명: `growth_log/README.md`
- 형식: 표 기반 Markdown  
- Notion “표 보기”로 임포트 시 자동 변환됨

---

## 🔗 3. Notion ↔ Git 연동 규칙

| 구분 | 설명 |
|------|------|
| 📘 **Notes** | Git의 `sqld/notes/` 폴더에서 작성 후 Notion에 업로드 |
| 📗 **Growth Log** | `growth_log/README.md`의 표를 Notion 표로 동기화 |
| 🎓 **Certifications** | SQLD Dashboard의 학습 단계별 목표 연결 |
| 🧭 **링크 규칙** | `[📄 dayNN_주제명](../sqld/notes/dayNN_주제명.md)` 형식 유지 |

---

## 📅 4. 워크플로우
```
1️⃣ Day 학습 진행  
2️⃣ Markdown 작성 및 정리  
3️⃣ Git 커밋 및 푸시  
4️⃣ Notion Growth Log 반영
```
> 매일 1회 커밋 원칙. 진척이 없을 경우 `chore(daily): maintenance log`로 일일 기록 유지.

---

## 🧠 5. 관리 원칙
| 규칙 | 설명 |
|------|------|
| 🕒 매일 1회 커밋 | 학습 지속성 확보 |
| 📂 폴더 일관성 | `notes` / `growth_log` 구분 명확 |
| ✏️ 커밋 메시지 통일 | `(chore/log/daily)` prefix 사용 |
| 🌱 Notion ↔ Git 동기화 | Markdown → Notion Import (드래그 앤 드롭) |
| 🔄 백업 원칙 | GitHub 기준으로 버전 관리 (Notion은 프런트 대시보드 역할) |

---

## 💡 Notion 업로드 방법
1️⃣ Notion 메인 페이지에서 `/import` 선택  
2️⃣ **Markdown & CSV** → `AI_Tech_Study_Hub_Setup.md` 선택  
3️⃣ 혹은 **파일 드래그 앤 드롭**으로 자동 변환  
4️⃣ 페이지 속성(아이콘·태그)만 수동으로 재지정

---

## 📘 6. 커밋 예시
```bash
git add sqld/notes/day06_정규화.md
git commit -m "chore(log): add SQLD Day 06 – 정규화 절차 및 BCNF (2025-10-18)"
git push origin main
```

---

> ✅ 이 문서는 `AI & Tech Study Hub`의 메인 구조 및 연동 기준 문서로,  
> GitHub와 Notion을 모두 병행 운영할 때 반드시 최신 버전을 유지해야 합니다.
