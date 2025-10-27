# **SQLD Day 15 – 다중행 서브쿼리 및 복합 쿼리 응용 (2025-10-27)**
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**
- 다중행 서브쿼리의 개념과 연산자 이해  
- EXISTS, IN, ANY, ALL 연산자의 차이 숙지  
- 복합 쿼리(UNION, INTERSECT, MINUS)의 작동 원리 및 활용 실습

---

## **🧠 이론 정리**

### **1️⃣ 다중행 서브쿼리의 개념**
> 다중행 서브쿼리(Multi-row Subquery)는 **여러 행(Row)** 을 반환하며,  
> 메인쿼리에서 다중 비교 연산자와 함께 사용된다.

| 구분 | 설명 | 예시 |
|------|------|------|
| **IN** | 여러 행 중 하나라도 일치하면 TRUE | `sal IN (SELECT sal FROM emp WHERE deptno=10)` |
| **ANY(SOME)** | 서브쿼리의 어떤 값이라도 만족하면 TRUE | `sal > ANY(SELECT sal FROM emp WHERE deptno=30)` |
| **ALL** | 모든 값과 비교해 조건을 만족해야 TRUE | `sal > ALL(SELECT sal FROM emp WHERE deptno=30)` |

> 💡 다중행 서브쿼리의 결과가 0건이면 **FALSE**를 반환한다.

---

### **2️⃣ EXISTS / NOT EXISTS**
> EXISTS는 서브쿼리 결과의 존재 여부만 확인하며, 실제 값은 반환하지 않는다.

```sql
SELECT deptno, dname
FROM dept d
WHERE EXISTS (SELECT 1 FROM emp e WHERE e.deptno = d.deptno);
```

| 구분 | 설명 | 예시 |
|------|------|------|
| **EXISTS** | 서브쿼리 결과가 존재하면 TRUE | `EXISTS (SELECT * FROM emp WHERE deptno=10)` |
| **NOT EXISTS** | 서브쿼리 결과가 존재하지 않으면 TRUE | `NOT EXISTS (SELECT * FROM emp WHERE deptno=40)` |

> ⚙️ EXISTS는 **상관 서브쿼리**와 함께 사용될 때 성능 최적화 효과가 크다.

---

### **3️⃣ 복합 쿼리 (UNION / INTERSECT / MINUS)**
> 복합 쿼리(Set Operation)는 **두 개 이상의 SELECT 결과를 결합**하여 하나의 결과로 반환한다.

| 연산자 | 설명 | 예시 |
|---------|------|------|
| **UNION** | 두 결과를 합집합으로 결합 (중복 제거) | `SELECT empno FROM emp1 UNION SELECT empno FROM emp2` |
| **UNION ALL** | 중복 포함 합집합 | `SELECT empno FROM emp1 UNION ALL SELECT empno FROM emp2` |
| **INTERSECT** | 교집합 결과 반환 | `SELECT deptno FROM emp INTERSECT SELECT deptno FROM dept` |
| **MINUS (EXCEPT)** | 첫 번째 결과에서 두 번째 결과 제외 | `SELECT deptno FROM emp MINUS SELECT deptno FROM dept` |

> 💡 복합 쿼리의 SELECT 절은 **컬럼 수와 데이터 타입이 동일**해야 한다.

---

### **4️⃣ ROLLUP / CUBE / GROUPING**
> GROUP BY 확장 기능으로, **다차원 요약 통계**를 수행할 수 있다.

| 함수 | 설명 | 예시 |
|------|------|------|
| **ROLLUP** | 상위 수준까지 누적 합계 계산 | `GROUP BY ROLLUP(deptno, job)` |
| **CUBE** | 가능한 모든 조합으로 합계 계산 | `GROUP BY CUBE(deptno, job)` |
| **GROUPING()** | ROLLUP/CUBE 결과 구분 | `SELECT deptno, job, GROUPING(job)` |

> ⚙️ ROLLUP은 **계층적 요약**, CUBE는 **모든 조합 요약**에 사용된다.

---

## **⚙️ 모델링 유의사항**
1. 다중행 서브쿼리는 집계 결과와 함께 사용할 때 결과 일관성 주의  
2. 복합 쿼리의 컬럼 수와 데이터 타입이 반드시 일치해야 함  
3. ROLLUP / CUBE는 대용량 데이터에서는 성능 영향이 크므로 실행 계획 검토 필요

---

## **⚙️ 핵심 요약**
- 다중행 서브쿼리는 **IN / ANY / ALL** 연산자와 함께 사용된다.  
- EXISTS는 “존재 여부”만 평가하며, 조건 검증에 효율적이다.  
- UNION, INTERSECT, MINUS를 통해 SQL 결과를 집합 기반으로 처리할 수 있다.  
- ROLLUP, CUBE는 데이터 분석용 다차원 통계 산출에 유용하다.

---

## **🧮 예제 및 실습**
**예제 1️⃣ – ANY / ALL 비교 연산**
```sql
SELECT ename, sal
FROM emp
WHERE sal > ALL (SELECT sal FROM emp WHERE deptno = 30);
```

**예제 2️⃣ – EXISTS 사용**
```sql
SELECT d.deptno, d.dname
FROM dept d
WHERE EXISTS (SELECT 1 FROM emp e WHERE e.deptno = d.deptno);
```

**예제 3️⃣ – UNION / INTERSECT / MINUS**
```sql
SELECT deptno FROM emp
UNION
SELECT deptno FROM dept;
```

- [x] ANY / ALL 서브쿼리 실습  
- [x] EXISTS / NOT EXISTS 성능 비교  
- [x] UNION / INTERSECT / MINUS 결과 비교  
- [ ] ROLLUP / CUBE 확장 실습 예정

---

## **🧾 기출 복습**
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2023 2회 | Q71–Q75 | ANY / ALL / EXISTS 비교 | ✅ | EXISTS 성능 최적화 확인 |
| 2022 1회 | Q66–Q70 | UNION / INTERSECT / MINUS | ⚠ | 컬럼 수 불일치 오류 주의 |
| 2021 2회 | Q61–Q65 | ROLLUP / CUBE 함수 | ✅ | GROUPING 결과 확인 |

> 📘 **기출 출처:**  
> SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ **기출예상문제 2-9절~2-10절 (p.186~200)** 기반 정리

---

## **💬 느낀점 / 메모**
- ANY / ALL / EXISTS의 차이를 실습으로 익히니 SQL의 논리 구조가 확실히 정리됐다.  
- 복합 쿼리는 데이터 병합 시 매우 강력하지만, 정렬 기준 통일이 중요하다.  
- GROUP BY 확장 기능(ROLLUP, CUBE)은 실제 데이터 분석에서 필수적임을 실감했다.

---

## **🔗 참고자료**
- 아이리포 SQLD 강의 – 2과목 15~17강 (유튜브 15~17강): 다중행 서브쿼리 및 복합 쿼리 응용  
- SQLD 공식 교재 2권 p.145~164, p.186~200 (기출예상문제)  
- [서브쿼리와 집합 연산자 – SQLGate 블로그](https://www.sqlgate.com/blog/sql-multi-row-subquery-union)
