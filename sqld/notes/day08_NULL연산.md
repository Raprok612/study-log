# **SQLD Day 08 – NULL 연산 및 처리 (2025-10-20)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**
- NULL의 의미 및 연산 규칙 이해  
- NULL 비교 연산 시 주의사항 숙지  
- NVL, COALESCE, NULLIF 등 NULL 처리 함수 활용  

---

## **🧠 이론 정리**

### **1️⃣ NULL의 개념**

NULL은 **값이 존재하지 않음 / 알 수 없음(Unknown)** 을 의미하는 **상태값**이다.

| 값 | 의미 | 예시 |
|---|---|---|
| **0** | 숫자 값 존재 | 연산 가능 |
| **''(빈문자열)** | 길이가 0인 문자열 | 문자열 처리 가능 |
| **NULL** | 값이 존재하지 않음 | 연산·비교 불가 |

> 💡 `NULL = NULL` → FALSE  
> 💡 `NULL IS NULL` → TRUE  

NULL은 데이터가 “없음”이 아니라 **판단 불가 상태**다.

---

### **2️⃣ NULL 연산 규칙**

| 연산 | 결과 |
|---|---|
| 10 + NULL | NULL |
| NULL * 5 | NULL |
| NULL = NULL | FALSE |
| NULL IS NULL | TRUE |

- 산술연산 포함 시 결과는 **항상 NULL**
- GROUP 함수는 NULL 제외  
  (단, `COUNT(*)` 는 NULL 포함 전체 행 수 계산)

---

### **3️⃣ NULL 관련 함수**

| 함수 | 설명 | 예시 |
|---|---|---|
| **NVL(a, b)** | a가 NULL이면 b 반환 | `NVL(comm, 0)` |
| **COALESCE(a, b, …)** | 첫 번째 NULL이 아닌 값 반환 | `COALESCE(bonus, comm, 0)` |
| **NULLIF(a, b)** | a=b이면 NULL 반환 | `NULLIF(grade,'A')` |

- NVL은 **Oracle 전용**  
- COALESCE는 **표준 SQL**, 다중 인자 가능  
- NULLIF는 비교 시 특정 값을 NULL 처리할 때 사용

---

### **📌 NULL – 단일행 vs 다중행**

- 단일행 연산  
  `100 + NULL = NULL`
- 다중행 집계  
  `AVG(10, 20, NULL, 30) = (10+20+30) / 3 = 20`  
  → NULL은 **집계에서 제외**

---

## **🧮 예제 및 실습**

```sql
SELECT empno, sal,
       NVL(comm, 0)   AS comm_adj,
       COALESCE(comm, bonus, 0) AS comm_final
FROM emp
WHERE NVL(comm, 0) > 0;
```

- [x] NVL / COALESCE 비교  
- [x] NULL 비교 테스트  
- [ ] NULLIF 활용 예제 추가 예정  

---

## **⚙️ 핵심 요약**

- NULL은 “모름(Unknown)” 상태값이며 연산·비교 불가  
- 비교는 반드시 **IS NULL / IS NOT NULL**  
- 산술연산에 NULL 포함 시 결과는 항상 NULL  
- NVL은 Oracle 전용, COALESCE는 표준 SQL  
- 집계 함수는 NULL을 제외하고 계산  

---

## **🧾 기출 복습**

| 회차 | 문항 | 주제 | 결과 | 비고 |
|---|---|---|---|---|
| 2023 2회 | Q36–Q40 | NULL 연산, NVL/COALESCE | ✅ | NVL/COALESCE 구분 중요 |
| 2022 1회 | Q31–Q35 | NULL 비교 및 집계 처리 | ⚠ | COUNT(NULL) 처리 주의 |

---

## **💬 느낀점 / 메모**

- NULL은 단순한 “빈값” 개념이 아니라 데이터의 **상태를 설명하는 의미적 값**이다.  
- NULL 처리 방식이 DBMS마다 다를 수 있으므로 항상 주의해야 한다.  
- WHERE 절 NULL 비교는 실수하기 쉬우므로 테스트 습관을 가져야겠다.

---

## **🔗 참고자료**
- 아이리포 SQLD 강의 – 2과목 8강  
- SQLD 공식 교재 2권 p.12~28, 122~129  
