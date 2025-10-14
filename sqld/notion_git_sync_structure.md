# 🨭 Notion ↔ Git Sync Structure Guide
> SQLD 학습 기록용 Notion 페이지와 GitHub 저장소의 1:1 대응 구조 가이드  
> 기준일: 2025-10-14  
> 작성자: Jaerok Kim (Raprok612)

---

## 🧩 전체 개요

이 문서는 **Notion** 에서 정리한 학습 페이지와  
**GitHub / VSCode** 상의 Markdown 파일을 일관성 있게 유지하기 위한 기준입니다.

| 구분 | 역할 | 편집 위치 | 저장 형태 |
|------|------|------------|------------|
| **Notion** | 기록/정리 UI | Notion 페이지 | 시각적 구조 (Heading + Page) |
| **VSCode** | 텍스트 편집기 | 로컬 파일 | Markdown(.md) |
| **GitHub** | 백업/이력 관리 | 리포지토리 | Commit/Push로 관리 |

---

## 📘 1. Notion 페이지 구조 (현재)

```
🎓 Certifications
 └── 🧭 SQLD Study Dashboard
      ├── ## 🗓️ Day별 학습 기록  ← 제목(Heading, 트리에 안 보임)
      ├── 📄 Day 01 – 모델링
      ├── 📄 Day 02 – 정규화
      ├── 📄 Day 03 – SQL 기초
      └── 📄 Day 04 – SQL 응용
```

| 아이콘 | 유형 | 설명 |
|--------|------|------|
| 📄 | Page | 실제 하위 페이지 (트리에 표시됨) |
| ## | Heading | 시각적 구분용 제목 (트리에 안 표시됨) |

---

## 🧱 2. GitHub / VSCode 폴더 구조

```
study-log/
 └── sqld/
      ├── reference/
      │    └── sqld_1과목_요약노트.md
      ├── notes/
      │    ├── day01_모델링.md
      │    ├── day02_정규화.md
      │    ├── day03_sql기초.md
      │    └── day04_sql응용.md
      └── sqld_study_dashboard.md
```

> 💡 Git에서는 모든 파일명을 **소문자 + 언더스코어(_)** 로 통일합니다.  
> Notion의 `Day 01 – 모델링` 페이지는 Git의 `day01_모델링.md`와 1:1 대응됩니다.

---

## 🔁 3. Notion → Git 반영 절차

1️⃣ **Notion에서 작성**  
- `SQLD Study Dashboard` → “Day 01 – 모델링” 페이지에 기록

2️⃣ **Markdown Export**  
- Notion 상단 `⋯` → `Export` → “Markdown & CSV” 선택  
- ZIP 파일 생성됨 → 압축 해제

3️⃣ **VSCode에서 교체**  
- 해제된 `.md` 파일을 기존 `study-log/sqld/notes/day01_모델링.md`에 덮어쓰기

4️⃣ **Git Commit**  
```bash
git add sqld/notes/day01_모델링.md
git commit -m "chore(log): update Day 01 – 모델링 from Notion (YYYY-MM-DD)"
git push
```

---

## 🤡 4. 파일명 및 페이지명 매칭표

| Notion 페이지명 | Git 파일명 | 비고 |
|-----------------|-------------|------|
| Day 01 – 모델링 | `day01_모델링.md` | 모델링 기초 |
| Day 02 – 정규화 | `day02_정규화.md` | 정규화 |
| Day 03 – SQL 기초 | `day03_sql기초.md` | SELECT, JOIN 복습 |
| Day 04 – SQL 응용 | `day04_sql응용.md` | 실무형 문제 |
| SQLD Study Dashboard | `sqld_study_dashboard.md` | 전체 개요 |
| SQLD 1과목 요약노트 | `reference/sqld_1과목_요약노트.md` | 과목별 개념 |

---

## 🧠 5. 유지 원칙

1. **파일명은 Git 기준 소문자 유지**  
2. **Notion은 시각적으로 가능한 Title Case 유지**  
3. **Import 보다는 복사-붙여넣기 방식 사용**  
4. **주 1회 백업 (가능한 Notion → VSCode → GitHub)**

---

## 🤩 6. 확장 계획

| 구분 | 목적 | 경로 |
|------|------|------|
| InfoProc | 정보처리기사 학습 | `study-log/infoproc/` |
| Network | 네트워크 기초 | `study-log/network/` |
| Bootcamp | AI Bootcamp 기록 | `study-log/bootcamp/` |

---

## ✅ 결론

| 역할 | Notion | Git |
|------|---------|-----|
| 작성 / 정리 | ✅ | ❌ |
| 편집 / 백업 | ✅ | ✅ |
| 이력 관리 | ❌ | ✅ |
| 공유 / 시각화 | ✅ | ⚙️ |

> 📍 **Notion은 기록 공간, Git은 보존 공간으로 구분하면 가장 안정적입니다.**
