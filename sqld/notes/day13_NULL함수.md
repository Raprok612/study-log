# **SQLD Day 13 – NULL 관련 함수 (NVL / NULLIF / COALESCE) (2025-10-25)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- NULL 처리 함수의 동작 방식 이해  
- NVL, NULLIF, COALESCE의 차이점 정확히 구분  
- 단일행/다중행 연산에서 NULL 처리 규칙 숙지  

---

## 🧠 이론 정리

### 1️⃣ NULL의 기본 개념
- **NULL = 값이 없음 / 모름(Unknown)**  
- `NULL = NULL` → ❌ FALSE  
- 반드시 `IS NULL` / `IS NOT NULL` 로 비교  

---

## 2️⃣ NVL / COALESCE / NULLIF 비교

| 함수 | 설명 | 예시 |
|------|------|------|
| **NVL(expr1, expr2)** | expr1이 NULL이면 expr2 반환 (Oracle 전용) | `NVL(comm, 0)` |
| **COALESCE(e1, e2, …)** | 첫 번째 NOT NULL 값을 반환 (표준 SQL) | `COALESCE(bonus, comm, 0)` |
| **NULLIF(a, b)** | a=b이면 NULL 반환 | `NULLIF(sal, 0)` |

> COALESCE는 NVL을 완전히 포함하는 상위 함수.  

---

## 3️⃣ NULL 연산 규칙

| 연산 | 결과 |
|------|------|
| 10 + NULL | NULL |
| NULL * 5 | NULL |
| AVG(10, 20, NULL, 30) | (10+20+30)/3 = 20 |

---

## 🧮 실습

```sql
SELECT 
  NVL(comm, 0) AS comm_adj,
  COALESCE(bonus, comm, 0) AS bonus_final,
  NULLIF(sal, 0) AS sal_checked
FROM emp;
```

---

## 💬 느낀점
- NULLIF는 실전에서 값 비교 후 조건 분기 처리 시 유용  
- NVL은 Oracle 전용이라 범용성은 COALESCE가 더 좋음  
- GROUP 함수에서 NULL 제외되는 부분이 자주 혼동됨  

---

## 🔗 참고자료
- 아이리포 SQLD 강의 – 13강  
- SQLD 공식 교재 2권 p.157~167
