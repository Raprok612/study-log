# SQLD Day 19 – 정규표현식 / 복합 쿼리 예제 (2025-10-31)

> 날짜: 2025-10-31  
> 학습자: Jaerok Kim (Raprok612)  
> 강의: 27~29강  
> 주제: 정규표현식 / 복합 쿼리 예제  

---

## 🎯 학습 목표

- SQL 내 정규표현식(Regular Expression) 문법 이해 및 패턴 매칭 활용
- 복합 쿼리(CASE, DECODE, 복합 조건)의 실제 적용 예제 학습
- 실무형 데이터 필터링 및 문자열 검증 로직 설계 능력 향상

---

## 🧠 이론 정리

### 🔹 1. 정규표현식 기본 문법

| 패턴 | 의미 | 예시 |
|------|------|------|
| `^` | 문자열의 시작 | `^A` → A로 시작 |
| `$` | 문자열의 끝 | `A$` → A로 끝 |
| `.` | 임의의 한 문자 | `A.B` → A, 아무 문자, B |
| `*` | 0개 이상 반복 | `A*` → A가 0번 이상 반복 |
| `+` | 1개 이상 반복 | `A+` → A가 1번 이상 반복 |
| `[]` | 문자 집합 | `[0-9]`, `[A-Z]` |
| `|` | OR 연산자 | `(ABC|DEF)` → ABC 또는 DEF |
| `()` | 그룹 | `(ab)+` → ab 반복 |

**활용 예시**
```sql
SELECT *
FROM CUSTOMER
WHERE REGEXP_LIKE(PHONE, '^010-[0-9]{4}-[0-9]{4}$');
```

> ☑️ 전화번호 형식 검증, 이메일 유효성 검증 등에 자주 사용됨.

---

### 🔹 2. 복합 쿼리 (CASE, DECODE, 조건문)

**CASE 문 기본형**
```sql
SELECT NAME,
       CASE
           WHEN SALARY >= 5000 THEN 'HIGH'
           WHEN SALARY BETWEEN 3000 AND 4999 THEN 'MID'
           ELSE 'LOW'
       END AS SAL_GRADE
FROM EMP;
```

**DECODE 함수**
```sql
SELECT DECODE(GRADE, 'A', 'Excellent', 'B', 'Good', 'C', 'Average', 'Unknown')
FROM STUDENT;
```

> ☑️ 조건 분기 로직을 SQL 내에서 처리할 때 유용.  
> ☑️ 복합 쿼리는 “조건 처리 + 결과 분류 + 문자열 검증”이 핵심.

---

## ⚙️ 모델링 유의사항

- 정규표현식 기반 검증 로직은 **응용 계층보다는 데이터 무결성 보조** 용도로 사용.  
- 복합 조건식은 **CASE WHEN > DECODE > IF** 순으로 가독성 유지.  
- SQL 내 논리 복잡도가 높아질수록, **뷰(View)** 혹은 **임시 테이블**로 분리 설계.  
- 입력값 검증은 DB와 APP 간 **중복 방지 설계** 필요.  

---

## 🧮 실습 예제

### ✅ 1. 이메일 검증
```sql
SELECT EMAIL
FROM USERS
WHERE REGEXP_LIKE(EMAIL, '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$');
```

### ✅ 2. 급여 등급 분류
```sql
SELECT EMPNO, ENAME, SAL,
       CASE
           WHEN SAL >= 5000 THEN 'A등급'
           WHEN SAL >= 3000 THEN 'B등급'
           ELSE 'C등급'
       END AS SAL_GRADE
FROM EMP;
```

### ✅ 3. 문자열 패턴 필터링
```sql
SELECT PRODUCT_NAME
FROM PRODUCTS
WHERE REGEXP_LIKE(PRODUCT_NAME, '(Pro|Max)$');
```

---

## 🧾 기출 포인트

| 구분 | 출제 유형 | 키워드 |
|------|------------|---------|
| 실무형 | 정규표현식 검증 | `REGEXP_LIKE`, `^`, `$`, `{}` |
| 개념형 | CASE / DECODE 차이 | “CASE는 범위, DECODE는 단일값 비교” |
| 응용형 | 문자열 조건 쿼리 | 패턴 + 조건식 혼합 문제 |

> 💡 기출에서는 “정규표현식 검증 조건 + CASE문”이 결합된 형태 자주 등장.

---

## 💬 느낀점

정규표현식은 SQLD에서 등장 빈도는 낮지만, **데이터 정합성 검증** 및 **실무형 필터링**에서 강력한 도구였다.  
복합 쿼리(CASE / DECODE)는 로직 흐름 제어에 핵심적인 구문으로,  
파이썬의 if-else 문과 동일한 사고 구조로 이해하니 훨씬 명확하게 다가왔다.

---

## 🔗 참고자료

- SQLD 공식 교재 Chapter 5 (문자열 함수 및 패턴 매칭)
- DataEdu SQLD 강의 27~29강
- Oracle SQL Developer Docs – REGEXP_LIKE
- https://docs.oracle.com/en/database/oracle/oracle-database/

---
