# SQLD Day 13 – 서브쿼리 (Subquery) 개념 및 활용 (2025-10-25)
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- 서브쿼리의 개념과 동작 순서 이해  
- 단일행 / 다중행 / 상관(상호연관) / EXISTS 서브쿼리의 차이 숙지  
- SELECT / FROM / WHERE / HAVING 내 서브쿼리 활용 패턴 학습  
- EXISTS와 IN의 성능 차이 이해  

---

## 🧠 이론 정리

### 1️⃣ 서브쿼리 개념
> 하나의 SQL문 안에 포함된 또 다른 SELECT문

- 메인쿼리보다 **먼저 실행**되어 결과를 반환  
- 결과는 메인쿼리의 조건식, 비교값, 혹은 테이블로 사용 가능  

```sql
SELECT name, salary
FROM employee
WHERE salary > (SELECT AVG(salary) FROM employee);
```

---

### 2️⃣ 서브쿼리의 종류

| 구분 | 결과 행 수 | 주요 연산자 | 설명 |
|------|-------------|-------------|------|
| **단일행 서브쿼리** | 1행 | =, >, <, >=, <= | 결과가 1행이 아닐 경우 오류 발생 |
| **다중행 서브쿼리** | N행 | IN, ANY, ALL | 여러 값 중 하나 이상 비교 |
| **상관 서브쿼리** | N행 | 메인쿼리 컬럼 참조 | 메인쿼리의 각 행마다 반복 수행 |
| **EXISTS 서브쿼리** | 존재 여부 | EXISTS / NOT EXISTS | 결과 존재 여부만 확인 (성능 유리) |

---

### 3️⃣ 위치별 활용

| 위치 | 설명 | 예시 |
|------|------|------|
| **WHERE절** | 조건 비교 | `salary > (SELECT AVG(salary) FROM employee)` |
| **FROM절 (인라인뷰)** | 임시 테이블로 활용 | `FROM (SELECT deptno, AVG(salary) AS avg_sal FROM emp GROUP BY deptno)` |
| **SELECT절** | 파생 컬럼 계산 | `SELECT name, (SELECT COUNT(*) FROM orders WHERE emp_id=e.id)` |
| **HAVING절** | 집계 조건 | `HAVING AVG(salary) > (SELECT AVG(salary) FROM employee)` |

---

## 🧮 예제 및 실습

```sql
-- 단일행
SELECT ename, sal FROM emp
WHERE sal > (SELECT AVG(sal) FROM emp);

-- 다중행
SELECT deptno, ename FROM emp
WHERE deptno IN (SELECT deptno FROM dept WHERE loc='SEOUL');

-- 상관 서브쿼리
SELECT e1.ename, e1.sal FROM emp e1
WHERE sal > (SELECT AVG(e2.sal) FROM emp e2 WHERE e1.deptno=e2.deptno);

-- EXISTS
SELECT d.dname FROM dept d
WHERE EXISTS (SELECT 1 FROM emp e WHERE e.deptno=d.deptno);
```

---

## ⚠️ 자주 하는 실수
- 단일행 결과에 `IN` 사용, 다중행 결과에 `=` 사용 → 오류  
- 상관 서브쿼리에서 메인 컬럼 누락 → 전체 비교 발생  
- EXISTS는 결과값이 아닌 **존재 여부**만 판단한다.  

---

## 🧾 기출 복습
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2024 1회 | Q41–Q45 | 단일행 / 다중행 서브쿼리 | ✅ | |
| 2023 2회 | Q46–Q50 | EXISTS vs IN 비교 | ⚠ | 성능 관련 문제 출제 |

---

## 💬 느낀점 / 메모
- 서브쿼리는 **데이터 흐름을 제어하는 핵심 문법**이다.  
- `EXISTS`는 IN보다 빠른 경우가 많다 (특히 대용량 테이블).  
- 상관 서브쿼리는 편리하지만, 실행 횟수가 많아 성능에 유의해야 한다.  

---

## 🔗 참고자료
- 아이리포 SQLD 강의 – 2과목 6강: 서브쿼리  
- SQLD 교재 2권 p.119~142  
- [서브쿼리 개념 및 활용 – SQLGate 블로그](https://www.sqlgate.com/blog/sql-subquery-guide)

