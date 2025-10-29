# **SQLD Day 16 – 서브쿼리 심화 및 중첩 쿼리 실습 (2025-10-28)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**

- 서브쿼리의 중첩 구조와 실행 순서 이해  
- EXISTS, IN, ANY, ALL 연산자의 심화 활용 실습  
- 서브쿼리의 성능 차이와 최적화 기법 학습

---

## **🧠 이론 정리**

### **1️⃣ 서브쿼리의 중첩 구조**

> 중첩 서브쿼리(Nested Subquery)는 SELECT, WHERE, FROM 절 등 다양한 위치에서 사용될 수 있다.

| 유형 | 설명 | 예시 |
|------|------|------|
| **WHERE 절 서브쿼리** | 조건식 내부에 포함 | `WHERE sal > (SELECT AVG(sal) FROM emp)` |
| **FROM 절 서브쿼리** | 인라인 뷰(임시 테이블)로 활용 | `FROM (SELECT deptno, AVG(sal) avg_sal FROM emp GROUP BY deptno)` |
| **SELECT 절 서브쿼리** | 계산값 반환 | `SELECT ename, (SELECT dname FROM dept WHERE deptno=e.deptno) AS dept_name` |

> 💡 **인라인 뷰**를 통해 서브쿼리를 독립적인 테이블처럼 사용할 수 있다.

---

### **2️⃣ EXISTS vs IN 성능 비교**

> EXISTS와 IN은 모두 “값 존재 여부”를 판단하지만, 내부 동작 방식에 따라 성능 차이가 존재한다.

| 항목 | EXISTS | IN |
|------|---------|----|
| **평가 방식** | 조건 만족 시 즉시 TRUE 반환 | 전체 결과를 모두 탐색 |
| **NULL 처리** | NULL 무시 | NULL 존재 시 결과 불확실 |
| **적합한 상황** | 대용량 상관 서브쿼리 | 소규모 데이터 비교 |

```sql
-- EXISTS 예시
SELECT d.deptno, d.dname
FROM dept d
WHERE EXISTS (SELECT 1 FROM emp e WHERE e.deptno = d.deptno);

-- IN 예시
SELECT d.deptno, d.dname
FROM dept d
WHERE d.deptno IN (SELECT deptno FROM emp);
```

> ⚙️ **대용량 데이터에서는 EXISTS가 일반적으로 더 빠르다.**

---

### **3️⃣ ANY / ALL 응용**

| 연산자 | 설명 | 예시 |
|---------|------|------|
| **ANY (SOME)** | 하나라도 만족하면 TRUE | `sal > ANY (SELECT sal FROM emp WHERE deptno=30)` |
| **ALL** | 모든 값보다 크거나 같아야 TRUE | `sal > ALL (SELECT sal FROM emp WHERE deptno=30)` |

> 💡 ANY는 “최솟값 기준 비교”, ALL은 “최댓값 기준 비교”로 이해하면 직관적이다.

---

### **4️⃣ 중첩 서브쿼리의 실행 순서**

1. 가장 안쪽 서브쿼리부터 실행됨  
2. 결과가 상위 쿼리로 전달되어 조건 평가  
3. 최종 SELECT 결과 반환

```sql
SELECT ename, sal
FROM emp
WHERE sal > (SELECT AVG(sal)
             FROM emp
             WHERE deptno = (SELECT deptno FROM dept WHERE dname='SALES'));
```

> ⚙️ 내부 서브쿼리가 많을수록 실행 비용이 증가하므로, 인라인 뷰로 분리하여 성능 최적화 가능

---
## **⚙️ 모델링 유의사항**

1. 서브쿼리 결과가 단일행임을 보장해야 함 (다중행 비교 연산자 사용 시 주의)  
2. SELECT 절의 스칼라 서브쿼리는 반복 수행으로 인한 성능 저하 가능성 주의  
3. 단일행 비교 연산 시 NULL 처리 방안(NVL, COALESCE)을 반드시 고려  
4. EXISTS / IN 조건은 인덱스 유무에 따라 실행 계획이 달라질 수 있음  
5. 인라인 뷰로 서브쿼리를 대체하면 가독성과 성능 모두 개선 가능

---

## **⚙️ 핵심 요약**

- 서브쿼리는 중첩 구조로 확장 가능하며, SELECT / FROM / WHERE 절 어디서든 사용 가능  
- EXISTS는 즉시 평가로 효율적, IN은 NULL 처리에 유의  
- ANY, ALL은 다중행 비교 시 사용되며, 서브쿼리의 결과 수에 따라 성능 차이 발생  
- 인라인 뷰로 복잡한 서브쿼리를 분리하면 가독성과 성능 모두 향상 가능

---

## **🧮 예제 및 실습**

**예제 1️⃣ – 중첩 서브쿼리 실습**
```sql
SELECT ename, sal
FROM emp
WHERE sal > (SELECT AVG(sal) FROM emp WHERE deptno = 30);
```

**예제 2️⃣ – EXISTS와 IN 비교**
```sql
SELECT deptno, dname
FROM dept d
WHERE EXISTS (SELECT 1 FROM emp e WHERE e.deptno = d.deptno);

SELECT deptno, dname
FROM dept d
WHERE deptno IN (SELECT deptno FROM emp);
```

**예제 3️⃣ – ANY / ALL 응용**
```sql
SELECT ename, sal
FROM emp
WHERE sal > ALL (SELECT sal FROM emp WHERE deptno=20);
```

- [x] 중첩 서브쿼리 구조 이해  
- [x] EXISTS / IN 성능 비교 실습  
- [x] ANY / ALL 연산자 응용 실습  

---

## **🧾 기출 복습**

| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2024 1회 | Q66–Q70 | EXISTS / IN 비교 | ✅ | EXISTS가 더 빠른 경우 확인 |
| 2023 2회 | Q61–Q65 | ANY / ALL 연산자 | ⚠ | ALL 조건 오답률 높음 |
| 2022 2회 | Q56–Q60 | 중첩 서브쿼리 실행 순서 | ✅ | 인라인 뷰 변환 가능성 |

> 📘 기출 출처: SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ **기출예상문제 2-11절~2-12절 (p.201~214)** 기반 정리

---

## **💬 느낀점 / 메모**

- EXISTS와 IN의 내부 처리 차이를 직접 비교하니 쿼리 최적화 감각이 생겼다.  
- 서브쿼리의 중첩 구조를 단계별로 풀어보니 SQL 실행 순서를 시각적으로 이해할 수 있었다.  
- 실무에서 복잡한 조건식은 인라인 뷰나 WITH절로 분리하면 훨씬 관리가 수월할 것 같다.

---

## **🔗 참고자료**

- 아이리포 SQLD 강의 – 2과목 18~20강 (유튜브 18~20강): 서브쿼리 심화 및 중첩 쿼리 실습  
- SQLD 공식 교재 2권 p.201~214 (서브쿼리 심화)  
- [SQL 서브쿼리 성능 비교 – SQLGate 블로그](https://www.sqlgate.com/blog/sql-subquery-exists-in)
