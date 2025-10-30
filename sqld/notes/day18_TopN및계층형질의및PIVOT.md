# **SQLD Day 18 – Top-N, 계층형 질의, PIVOT 실습 (2025-10-30)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**

- Top-N 쿼리 및 ROWNUM, LIMIT 절의 동작 원리 이해  
- 계층형 질의(Hierarchical Query) 구조 파악 및 실습  
- PIVOT / UNPIVOT을 활용한 행열 변환 기법 학습

---

## **🧠 이론 정리**

### **1️⃣ Top-N 쿼리**
> 상위 N개의 행만 추출하는 쿼리로, 성능 테스트나 보고서 작성 시 자주 활용된다.

| DBMS | 문법 | 예시 |
|------|------|------|
| Oracle | ROWNUM | `SELECT * FROM emp WHERE ROWNUM <= 5;` |
| MySQL / PostgreSQL | LIMIT | `SELECT * FROM emp ORDER BY sal DESC LIMIT 5;` |
| SQL Server | TOP | `SELECT TOP 5 * FROM emp ORDER BY sal DESC;` |

> 💡 ROWNUM은 WHERE 절보다 **먼저 평가**되므로, 정렬 후 추출 시 서브쿼리로 감싸야 함.

```sql
SELECT *
FROM (
    SELECT ename, sal FROM emp ORDER BY sal DESC
)
WHERE ROWNUM <= 3;
```

---

### **2️⃣ 계층형 질의 (Hierarchical Query)**

> 조직도나 카테고리 구조처럼 **상하위 관계 데이터**를 조회할 때 사용.

| 키워드 | 설명 |
|---------|------|
| **START WITH** | 루트 행 지정 |
| **CONNECT BY PRIOR** | 부모-자식 관계 지정 |
| **LEVEL** | 계층 깊이 표시 (1부터 시작) |

```sql
SELECT LEVEL, empno, ename, mgr
FROM emp
START WITH mgr IS NULL
CONNECT BY PRIOR empno = mgr;
```

> ⚙️ LEVEL 키워드로 들여쓰기나 계층 깊이 표현 가능.  

---

### **3️⃣ PIVOT / UNPIVOT**
> 행과 열을 전환하여 데이터를 가독성 있게 변형하는 기능.

| 기능 | 설명 | 예시 |
|------|------|------|
| **PIVOT** | 행 → 열 변환 | `PIVOT (SUM(sal) FOR deptno IN (10,20,30))` |
| **UNPIVOT** | 열 → 행 변환 | `UNPIVOT (sal FOR deptno IN (d10,d20,d30))` |

```sql
SELECT *
FROM emp
PIVOT (SUM(sal) FOR deptno IN (10,20,30));
```

> 💡 PIVOT은 주로 BI, 리포트용 SQL에서 많이 활용된다.

---

## **⚙️ 모델링 유의사항**

1. Top-N 쿼리는 ORDER BY 이후 실행 순서 주의 (ROWNUM은 정렬 전 평가됨)  
2. 계층형 질의는 SELF JOIN보다 성능이 우수하지만, 순환 참조(Loop)에 주의  
3. PIVOT은 집계 기반 변환이므로, 비집계 변환 시 UNION 사용 고려  
4. 계층형 구조를 설계할 때 부모-자식 관계의 **무결성 제약(FK)** 필요  
5. ROWNUM, LIMIT 사용 시 DBMS별 차이 고려 (이식성 주의)

---

## **⚙️ 핵심 요약**

- **Top-N**: 상위/하위 데이터 추출  
- **계층형 질의**: 조직도, 트리 구조 조회  
- **PIVOT / UNPIVOT**: 행열 변환 및 리포트용 쿼리 구성  
- **실무 팁**: ORDER BY + ROWNUM 조합 시 반드시 서브쿼리 필요

---

## **🧮 예제 및 실습**

**예제 1️⃣ – Top-N 급여자 조회**
```sql
SELECT *
FROM (
    SELECT ename, sal FROM emp ORDER BY sal DESC
)
WHERE ROWNUM <= 3;
```

**예제 2️⃣ – 계층형 질의 실습**
```sql
SELECT LEVEL, empno, ename, mgr
FROM emp
START WITH mgr IS NULL
CONNECT BY PRIOR empno = mgr;
```

**예제 3️⃣ – PIVOT 실습**
```sql
SELECT *
FROM emp
PIVOT (SUM(sal) FOR deptno IN (10,20,30));
```

- [x] Top-N 쿼리 정렬 순서 검증  
- [x] 계층형 질의 구조 분석  
- [x] PIVOT / UNPIVOT 변환 실습  

---

## **🧾 기출 복습**

| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2024 2회 | Q76–Q80 | ROWNUM / LIMIT 쿼리 | ✅ | 실행 순서 유의 |
| 2023 1회 | Q71–Q75 | 계층형 질의 | ⚠ | PRIOR 방향 오답률 높음 |
| 2022 2회 | Q66–Q70 | PIVOT / UNPIVOT | ✅ | 컬럼명 매칭 중요 |

> 📘 기출 출처: SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ **기출예상문제 2-15절~2-16절 (p.229~243)** 기반 정리

---

## **💬 느낀점 / 메모**

- Top-N 쿼리의 실행 순서와 서브쿼리 활용법을 명확히 이해했다.  
- 계층형 질의는 조직 구조나 카테고리 트리 표현에 매우 유용했다.  
- PIVOT 변환은 리포트 SQL에서 필수적인 기술임을 체감했다.

---

## **🔗 참고자료**

- 아이리포 SQLD 강의 – 2과목 24~26강 (유튜브 24~26강): Top-N, 계층형 질의, PIVOT  
- SQLD 공식 교재 2권 p.229~243  
- [SQL Top-N과 PIVOT – SQLGate 블로그](https://www.sqlgate.com/blog/sql-topn-pivot)
