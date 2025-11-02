# **SQLD Day 19 – 정규표현식, 복합 쿼리 예제 (2025-10-31)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**

- SQL 내 정규표현식(Regular Expression) 문법과 활용 이해  
- 복합 쿼리(CASE, DECODE, 조건 분기)의 실제 예제 분석  
- 문자열 검증 및 데이터 필터링 로직 설계 능력 강화

---

## **🧠 이론 정리**

### **1️⃣ 정규표현식 (Regular Expression)**

> SQL에서 문자열 패턴을 검증하거나 추출할 때 사용하는 문법

| 패턴 | 의미 | 예시 |
|------|------|------|
| `^` | 문자열의 시작 | `^A` → A로 시작 |
| `$` | 문자열의 끝 | `A$` → A로 끝 |
| `.` | 임의의 한 문자 | `A.B` → A, 아무 문자, B |
| `*` | 0개 이상 반복 | `A*` → A가 0번 이상 반복 |
| `+` | 1개 이상 반복 | `A+` → A가 1번 이상 반복 |
| `[]` | 문자 집합 | `[0-9]`, `[A-Z]` |
| `{n,m}` | n~m번 반복 | `[0-9]{4}` → 숫자 4자리 |
| `|` | OR 조건 | `(ABC|DEF)` → ABC 또는 DEF |

```sql
SELECT *
FROM CUSTOMER
WHERE REGEXP_LIKE(PHONE, '^010-[0-9]{4}-[0-9]{4}$');
```

> 💡 전화번호·이메일 등 문자열 형식 검증에 자주 사용됨.

---

### **2️⃣ 복합 쿼리 (CASE, DECODE, 조건문)**

| 구문 | 설명 | 예시 |
|------|------|------|
| **CASE** | 다중 조건 분기 | `CASE WHEN SAL >= 5000 THEN 'HIGH' WHEN SAL >= 3000 THEN 'MID' ELSE 'LOW' END` |
| **DECODE** | 단일 조건 비교 | `DECODE(GRADE, 'A','Excellent','B','Good','C','Average','Unknown')` |
| **복합 쿼리 응용** | CASE + GROUP BY + JOIN 등 결합 | `CASE WHEN JOB='SALESMAN' THEN COMM ELSE 0 END` |

```sql
SELECT ENAME,
       CASE 
           WHEN SAL >= 5000 THEN 'HIGH'
           WHEN SAL BETWEEN 3000 AND 4999 THEN 'MID'
           ELSE 'LOW'
       END AS SAL_GRADE
FROM EMP;
```

> ⚙️ 복합 조건문은 가독성과 유지보수성을 높이기 위해 CASE WHEN 사용을 권장.

---

## **⚙️ 모델링 유의사항**

1. 정규표현식 기반 검증은 **무결성 보조** 용도로 활용 (비즈니스 로직은 앱단 처리)  
2. 복합 조건식은 **CASE > DECODE > IF** 순으로 가독성 유지  
3. 로직이 길어지면 **뷰(View)** 나 **임시 테이블**로 분리  
4. REGEXP_LIKE는 DBMS마다 문법 차이 있음 (Oracle / MySQL 구분)  

---

## **🧮 예제 및 실습**

**예제 1️⃣ – 이메일 검증**  
```sql
SELECT EMAIL
FROM USERS
WHERE REGEXP_LIKE(EMAIL, '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$');
```

**예제 2️⃣ – 급여 등급 분류**  
```sql
SELECT EMPNO, ENAME, SAL,
       CASE
           WHEN SAL >= 5000 THEN 'A등급'
           WHEN SAL >= 3000 THEN 'B등급'
           ELSE 'C등급'
       END AS SAL_GRADE
FROM EMP;
```

**예제 3️⃣ – 문자열 패턴 필터링**  
```sql
SELECT PRODUCT_NAME
FROM PRODUCTS
WHERE REGEXP_LIKE(PRODUCT_NAME, '(Pro|Max)$');
```

- [x] REGEXP_LIKE 패턴 검증 실습  
- [x] CASE문 / DECODE문 비교  
- [x] 조건 분기형 복합 쿼리 작성

---

## **🧾 기출 복습**

| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2024 2회 | Q60–Q65 | 정규표현식 검증 | ✅ | 패턴 해석 정확 |
| 2023 1회 | Q55–Q60 | CASE / DECODE | ⚠ | 조건 순서 혼동 |
| 2022 2회 | Q50–Q54 | 문자열 필터링 | ✅ | REGEXP_LIKE 활용 |

> 📘 기출 출처: SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ 기출예상문제 2-13절~2-14절 (p.210~228)

---

## **💬 느낀점 / 메모**

- 정규표현식은 SQL에서도 문자열 패턴 검증에 강력한 도구였다.  
- CASE문은 로직이 명확하고 가독성이 좋아 실무 SQL에도 자주 쓰인다.  
- 복합 쿼리를 구조적으로 작성하는 습관이 필요함을 느꼈다.

---

## **🔗 참고자료**

- 아이리포 SQLD 강의 – 2과목 27~29강 (유튜브 27~29강): 정규표현식 / 복합 쿼리 예제  
- SQLD 공식 교재 2권 p.210~228  
- [Oracle REGEXP_LIKE Documentation](https://docs.oracle.com/en/database/oracle/oracle-database/)
