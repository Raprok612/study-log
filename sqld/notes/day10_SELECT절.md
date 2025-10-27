# **SQLD Day 10 – SELECT 절 구조 및 데이터 조회 기본 (2025-10-22)**
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**
- SELECT 문 구조 및 실행 순서 이해  
- FROM, WHERE, ORDER BY 절의 역할 학습  
- DISTINCT, ALIAS, LIMIT 등의 핵심 키워드 익히기  

---

## **🧠 이론 정리**

### **1️⃣ SELECT 문의 구조**
> SQL에서 데이터를 조회하기 위한 가장 기본적인 명령문으로,  
> SELECT 문은 아래와 같은 순서로 구성된다.

```sql
SELECT [DISTINCT] 컬럼명 [, 컬럼명2 ...]
FROM 테이블명
WHERE 조건식
GROUP BY 컬럼명
HAVING 그룹조건
ORDER BY 컬럼명 [ASC|DESC];
```

| 절(Clause) | 역할 | 실행 순서 |
|-------------|------|------------|
| FROM | 데이터를 가져올 테이블 지정 | 1 |
| WHERE | 조건에 맞는 행(Row) 필터링 | 2 |
| GROUP BY | 그룹화 기준 컬럼 정의 | 3 |
| HAVING | 그룹 조건 필터링 | 4 |
| SELECT | 필요한 컬럼 선택 | 5 |
| ORDER BY | 결과 정렬 | 6 |

> 💡 **SQL 실행 순서 핵심:** FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY

---

### **2️⃣ DISTINCT와 ALIAS**
| 구문 | 설명 | 예시 |
|------|------|------|
| **DISTINCT** | 중복된 행 제거 | `SELECT DISTINCT job FROM emp;` |
| **ALIAS (별칭)** | 컬럼/테이블에 별칭 지정 | `SELECT ename AS name FROM emp;` |

> ⚙️ 별칭(ALIAS)은 SQL 가독성을 높이고, 계산식 결과를 명확히 표현할 때 유용하다.

---

### **3️⃣ ORDER BY와 LIMIT**
- ORDER BY: 결과 정렬 (`ASC` 기본 오름차순, `DESC` 내림차순)  
  ```sql
  SELECT ename, sal FROM emp ORDER BY sal DESC;
  ```
- LIMIT / FETCH: 출력 행 수 제한  
  ```sql
  SELECT * FROM emp FETCH FIRST 5 ROWS ONLY;
  ```

> ⚠️ Oracle은 `ROWNUM`, MySQL은 `LIMIT`, SQL Server는 `TOP` 키워드를 사용한다.

---

## **⚙️ 모델링 유의사항**
1. SELECT 문은 항상 필요한 컬럼만 조회하여 성능 최적화할 것  
2. WHERE 조건은 인덱스 컬럼 중심으로 설계  
3. ORDER BY 다중 컬럼 정렬 시 순서에 따른 우선순위 주의  

---

## **⚙️ 핵심 요약**
- SELECT 문은 SQL의 기본이자 중심 명령어이다.  
- 실행 순서를 이해하면 복잡한 쿼리도 논리적으로 해석 가능하다.  
- DISTINCT, ALIAS, ORDER BY는 SQL 결과 가독성을 높이는 주요 키워드이다.  

---

## **🧮 예제 및 실습**
```sql
SELECT DISTINCT deptno, job
FROM emp
WHERE sal > 2000
ORDER BY deptno ASC;
```
- [x] DISTINCT 실습  
- [x] ORDER BY 정렬 실습  
- [ ] FETCH/LIMIT 행 제한 실습  

---

## **🧾 기출 복습**
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2023 2회 | Q46–Q50 | SELECT 실행 순서 | ✅ | FROM → WHERE → GROUP BY 순서 복습 |
| 2022 1회 | Q41–Q45 | DISTINCT / ORDER BY | ⚠ | LIMIT / FETCH 구문 차이 주의 |

> 📘 **기출 출처:**  
> SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ **기출예상문제 2-4절 (p.139~146)** 기반 정리

---

## **💬 느낀점 / 메모**
- SELECT 문 실행 순서를 이해하니 쿼리 해석이 훨씬 쉬워졌다.  
- WHERE와 HAVING의 차이를 구분하며 필터링 로직을 명확히 세울 수 있었다.  
- 불필요한 SELECT * 사용을 지양해야겠다는 점이 인상 깊었다.

---

## **🔗 참고자료**
- 아이리포 SQLD 강의 – 2과목 10강 (유튜브 10강): SELECT 절 구조  
- SQLD 공식 교재 2권 p.49~68, p.139~146 (기출예상문제)  
- [SELECT 문 구조와 실행 순서 – SQLGate 블로그](https://www.sqlgate.com/blog/sql-select-structure)
