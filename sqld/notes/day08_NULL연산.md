# SQLD Day 08 – NULL 연산 및 처리 (2025-10-20)
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- NULL의 의미 및 연산 규칙 이해  
- NULL 비교 연산 시 주의사항 숙지  
- NVL, COALESCE, ISNULL 등 NULL 처리 함수 활용

---

## 🧠 이론 정리

### 1️⃣ NULL의 개념
- 데이터가 존재하지 않거나 알 수 없음을 의미하는 **특수값**
- ‘0’, ‘공백(‘’)’, ‘FALSE’ 와는 다르다

> 💡 NULL은 값이 아니라 **“모름(Unknown)”** 상태

---

### 2️⃣ NULL 연산 규칙
| 연산 | 결과 |
|------|------|
| 10 + NULL | NULL |
| NULL * 5 | NULL |
| NULL = NULL | ❌ (FALSE) |
| NULL IS NULL | ✅ (TRUE) |

> ⚠️ NULL 비교 시 반드시 `IS NULL`, `IS NOT NULL` 사용해야 함

---

### 3️⃣ NULL 관련 함수
| 함수 | 설명 | 예시 |
|------|------|------|
| **NVL(expr1, expr2)** | expr1이 NULL이면 expr2 반환 | NVL(comm, 0) |
| **COALESCE(e1, e2, ...)** | 첫 번째 NULL이 아닌 값 반환 | COALESCE(bonus, comm, 0) |
| **ISNULL(expr, value)** | expr이 NULL이면 value 반환 (SQL Server) | ISNULL(comm, 0) |
| **NULLIF(a, b)** | a와 b가 같으면 NULL 반환 | NULLIF(grade, 'A') |

---

## 🧮 예제 및 실습
```sql
SELECT empno, sal, NVL(comm, 0) AS comm_adj
FROM emp
WHERE NVL(comm, 0) > 0;
```
- [x] NVL, COALESCE 실습
- [x] NULL 비교 연산 테스트
- [ ] NULLIF 함수 활용 예제 추가

---

## 🧾 기출 복습
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2023 2회 | Q31–Q35 | NULL 연산 개념 | ✅ | |
| 2022 1회 | Q26–Q30 | NVL / COALESCE 차이 | ⚠ | 함수 매개변수 순서 확인 필요 |

---

## 💬 느낀점 / 메모
- NULL은 “값이 없음”이 아니라 “모름”이라는 점을 항상 인식해야 한다.  
- NVL과 COALESCE는 거의 동일하지만 **COALESCE는 표준 SQL**임을 기억하자.  
- WHERE절에서의 NULL 비교는 예외 케이스가 많아 반드시 테스트해야 한다.

---

## 🔗 참고자료
- 아이리포 SQLD 강의 – 2과목 1강: NULL 연산  
- SQLD 교재 2권 p.12~29  
- [NVL / COALESCE 차이 정리 블로그](https://www.sqlgate.com/blog/sql-null-functions/)
