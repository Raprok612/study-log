# **SQLD Day 08 – NULL 연산 및 처리 (2025-10-20)**
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**
- NULL의 의미 및 연산 규칙 이해  
- NULL 비교 연산 시 주의사항 숙지  
- NVL, COALESCE, ISNULL 등 NULL 처리 함수 활용

---

## **🧠 이론 정리**

### **1️⃣ NULL의 개념**
> NULL은 데이터가 존재하지 않거나 알 수 없음을 의미하는 **특수한 상태값**이며,  
> ‘0’, ‘공백(‘’)’, ‘FALSE’와는 **전혀 다른 개념**이다.

| 구분 | 설명 | 예시 |
|------|------|------|
| **0** | 숫자 값 존재 | 수학적 계산 가능 |
| **공백('')** | 문자열 존재, 길이 0 | ' ' |
| **NULL** | 값이 존재하지 않음 | 산술/비교 불가 |

> 💡 NULL은 값이 아니라 “모름(Unknown)”의 상태로,  
> `NULL = NULL` → ❌ FALSE / `NULL IS NULL` → ✅ TRUE

---

### **2️⃣ NULL 연산 규칙**
| 연산 | 결과 |
|------|------|
| 10 + NULL | NULL |
| NULL * 5 | NULL |
| NULL = NULL | FALSE |
| NULL IS NULL | TRUE |

- 비교 시에는 반드시 `IS NULL`, `IS NOT NULL` 사용  
- GROUP 함수는 NULL 값을 제외하고 계산 (단, COUNT(*)는 예외)

---

### **3️⃣ NULL 관련 함수**
| 함수 | 설명 | 예시 |
|------|------|------|
| **NVL(expr1, expr2)** | expr1이 NULL이면 expr2 반환 | `NVL(comm, 0)` |
| **COALESCE(e1, e2, …)** | 첫 번째 NULL이 아닌 값 반환 | `COALESCE(bonus, comm, 0)` |
| **ISNULL(expr, value)** | expr이 NULL이면 value 반환 (SQL Server 전용) | `ISNULL(comm, 0)` |
| **NULLIF(a, b)** | a와 b가 같으면 NULL 반환 | `NULLIF(grade, 'A')` |

> 💡 NVL과 COALESCE는 유사하지만, **COALESCE는 표준 SQL 함수**이다.

---

## **🧮 예제 및 실습**
```sql
SELECT empno, sal, NVL(comm, 0) AS comm_adj
FROM emp
WHERE NVL(comm, 0) > 0;
```

- [x] NVL, COALESCE 실습 완료  
- [x] NULL 비교 연산 테스트  
- [ ] NULLIF 함수 활용 예제 추가

---

## **⚙️ 핵심 요약**
- NULL은 “값이 없음”이 아니라 “모름(Unknown)”의 상태이다.  
- 산술/비교 연산 시 NULL이 포함되면 결과도 NULL.  
- 비교는 반드시 **IS NULL / IS NOT NULL** 로 수행.  
- NVL은 Oracle 전용, COALESCE는 표준 SQL이며 다중 인자 처리 가능.  
- 실무에서는 NULL 정책을 명확히 문서화해야 한다.

---

## **🧾 기출 복습**
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2023 2회 | Q36–Q40 | NULL 연산, NVL/COALESCE 함수 | ✅ | NVL과 COALESCE의 차이 확인 |
| 2022 1회 | Q31–Q35 | NULL 비교 및 GROUP 함수 | ⚠ | COUNT와 NULL 처리 혼동 주의 |

> 📘 **기출 출처:**  
> SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ **기출예상문제 2-2절 (p.122~129)** 기반 정리

---

## **💬 느낀점 / 메모**
- NULL은 단순히 값이 없는 것이 아니라 **데이터 상태를 설명하는 의미적 개념**이다.  
- NVL과 COALESCE의 차이를 명확히 이해하고, DBMS별 동작 차이를 주의해야 한다.  
- WHERE절에서 NULL 비교 실수를 방지하기 위해 테스트 케이스를 작성하는 습관이 필요하다.

---

## **🔗 참고자료**
- 아이리포 SQLD 강의 – 2과목 8강 (유튜브 8강): NULL 연산 및 처리  
- SQLD 공식 교재 2권 p.12~28, p.122~129 (기출예상문제)  
- [NVL / COALESCE 차이 정리 블로그 – SQLGate](https://www.sqlgate.com/blog/sql-null-functions/)
