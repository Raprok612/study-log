# SQLD Day 14 – 단일행 서브쿼리 응용 및 WHERE절 비교연산 (2025-10-26)
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- 단일행 서브쿼리의 비교 연산자 응용  
- WHERE절에서의 서브쿼리 조건 제어  
- 평균, 최대, 최소값 비교 문제 해결 패턴 익히기  

---

## 🧠 이론 정리

### 1️⃣ 단일행 서브쿼리 복습
- 결과가 **정확히 1행**만 반환되어야 함  
- 비교 연산자 `=, >, <, >=, <=` 사용  

```sql
SELECT ename, sal
FROM emp
WHERE sal > (SELECT AVG(sal) FROM emp);
```

> 💡 여러 행이 반환되면 “ORA-01427: 단일행 하위 질의가 둘 이상의 행을 반환했습니다.” 오류 발생

---

### 2️⃣ 단일행 서브쿼리 응용 패턴

| 패턴 | 설명 | 예시 |
|------|------|------|
| **최대/최소값 비교** | 특정 기준 이상/이하의 행 찾기 | `sal = (SELECT MAX(sal) FROM emp)` |
| **비교 대상이 다른 테이블일 때** | 부서별 비교 등 | `WHERE sal > (SELECT AVG(sal) FROM emp WHERE deptno=10)` |
| **다중 조건 결합** | 서브쿼리 + 일반 조건 | `WHERE sal > (...) AND job='MANAGER'` |

---

### 3️⃣ 단일행 서브쿼리 실습 예제

```sql
-- 최고 급여자 조회
SELECT ename, sal
FROM emp
WHERE sal = (SELECT MAX(sal) FROM emp);

-- 부서 평균보다 급여가 높은 사원
SELECT ename, deptno, sal
FROM emp
WHERE sal > (SELECT AVG(sal) FROM emp WHERE deptno=10);
```

---

## 🧾 기출 복습
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2023 2회 | Q51–Q54 | 단일행 서브쿼리 비교연산 | ✅ | |
| 2022 1회 | Q46–Q49 | AVG / MAX / MIN 비교 | ⚠ | 오류 조건 확인 필요 |

---

## 💬 느낀점 / 메모
- 단일행 서브쿼리는 기본이지만 출제 빈도가 높다.  
- 비교 연산자와 서브쿼리 결과 행 수의 일치가 핵심 포인트.  
- SQL 실행 순서를 머릿속에 그리면 오류를 줄일 수 있다.  

---

## 🔗 참고자료
- 아이리포 SQLD 강의 – 2과목 7강: 단일행 서브쿼리 응용  
- SQLD 교재 2권 p.143~155  
- [단일행 서브쿼리 – SQLGate 블로그](https://www.sqlgate.com/blog/sql-single-row-subquery)
