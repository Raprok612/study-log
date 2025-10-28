# SQLD Day 16 – 서브쿼리 심화 및 중첩 쿼리 실습 (EXISTS, IN, ANY, ALL)
> 날짜: 2025-10-28  
> 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- EXISTS, IN, ANY, ALL 등의 **서브쿼리 조건식** 활용법 이해
- **중첩 서브쿼리**의 실행 순서 및 성능 고려사항 학습
- **다중행 비교 연산자**를 통한 실무형 쿼리 작성 능력 강화

---

## 🧠 이론 정리

### 1️⃣ EXISTS 서브쿼리
- 서브쿼리의 결과가 존재하면 TRUE를 반환.
```sql
SELECT *
FROM EMP e
WHERE EXISTS (SELECT 1 FROM DEPT d WHERE e.DEPTNO = d.DEPTNO);
```

### 2️⃣ IN / NOT IN
- 단일 컬럼의 값 비교에 주로 사용.
- NULL 값 존재 시 주의 필요.

```sql
SELECT *
FROM EMP
WHERE DEPTNO IN (SELECT DEPTNO FROM DEPT WHERE LOC = 'DALLAS');
```

### 3️⃣ ANY / ALL
- ANY: 하나라도 조건을 만족하면 TRUE  
- ALL: 모든 조건을 만족해야 TRUE

```sql
SELECT *
FROM EMP
WHERE SAL > ALL (SELECT SAL FROM EMP WHERE DEPTNO = 30);
```

---

## ⚙️ 핵심 요약

| 구분 | 의미 | 사용 예시 |
|------|------|------------|
| EXISTS | 존재 여부 확인 | WHERE EXISTS (subquery) |
| IN | 특정 목록 포함 여부 | WHERE COL IN (subquery) |
| ANY | 하나라도 조건 만족 | > ANY (subquery) |
| ALL | 모든 조건 만족 | > ALL (subquery) |

---

## 🧮 실습 예시

```sql
-- 부서가 존재하는 직원만 출력
SELECT ENAME, DEPTNO
FROM EMP e
WHERE EXISTS (SELECT 1 FROM DEPT d WHERE e.DEPTNO = d.DEPTNO);

-- 부서별 최고 급여자 조회 (ALL 사용)
SELECT ENAME, SAL, DEPTNO
FROM EMP
WHERE SAL >= ALL (SELECT SAL FROM EMP e2 WHERE e2.DEPTNO = EMP.DEPTNO);
```

---

## 🧾 기출 복습
- EXISTS와 IN의 성능 차이는 **인덱스 존재 여부**에 따라 다름  
- ANY/ALL 문제는 “부등호 방향”에 유의해야 함

---

## 💬 느낀점
서브쿼리 구조를 명확히 이해하니 복잡해 보이던 SQL 문장이 읽히기 시작했다.  
특히 EXISTS와 IN의 내부 처리 차이를 시각적으로 이해하면, 실무에서 성능 튜닝 시 매우 유용할 듯하다.

---

## 🔗 참고 자료
- SQLD 공식 교재: SQL 기본 및 응용 (18~20강)
- [SQLGate 블로그 – EXISTS vs IN 비교](https://www.sqlgate.com/blog/sql-exists-vs-in)
