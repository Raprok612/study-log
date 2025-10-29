# **SQLD Day 17 – GROUPING 및 윈도우 함수 (2025-10-29)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**

- GROUP BY 확장 문법(GROUPING SETS, ROLLUP, CUBE) 완전 이해  
- 윈도우 함수(OVER, PARTITION BY, ORDER BY) 개념 및 응용  
- 순위 함수(RANK, DENSE_RANK, ROW_NUMBER)의 차이와 활용 실습

---

## **🧠 이론 정리**

### **1️⃣ GROUP BY 확장 기능**

> GROUPING SETS, ROLLUP, CUBE는 집계 분석을 다차원적으로 확장하는 핵심 문법이다.

| 함수 | 설명 | 예시 |
|------|------|------|
| **GROUPING SETS** | 여러 그룹 조합을 개별적으로 계산 | `GROUP BY GROUPING SETS ((deptno), (job))` |
| **ROLLUP** | 단계별 누적 집계 (상위 수준 포함) | `GROUP BY ROLLUP (deptno, job)` |
| **CUBE** | 가능한 모든 조합의 요약 통계 | `GROUP BY CUBE (deptno, job)` |

```sql
SELECT deptno, job, SUM(sal)
FROM emp
GROUP BY ROLLUP (deptno, job);
```

> 💡 ROLLUP은 “계층적 요약”, CUBE는 “모든 조합 요약”으로 기억.

---

### **2️⃣ GROUPING() 함수**

> ROLLUP / CUBE의 결과를 구분하기 위한 보조 함수로,  
> 집계된 결과(상위 요약행)는 1, 일반 데이터는 0을 반환한다.

```sql
SELECT deptno, job, SUM(sal),
       GROUPING(deptno) AS g_dept,
       GROUPING(job) AS g_job
FROM emp
GROUP BY ROLLUP (deptno, job);
```

| 반환값 | 의미 |
|---------|------|
| **0** | 실제 데이터 행 |
| **1** | 요약(집계) 행 |

---

### **3️⃣ 윈도우 함수 (Window Function)**

> 윈도우 함수는 **집계 결과를 각 행 단위로 나눠 계산**할 수 있는 함수다.

| 구성 요소 | 설명 |
|-------------|------|
| **OVER()** | 윈도우 함수 정의 영역 |
| **PARTITION BY** | 그룹 기준 |
| **ORDER BY** | 정렬 기준 |

```sql
SELECT ename, deptno, sal,
       SUM(sal) OVER (PARTITION BY deptno) AS dept_sum
FROM emp;
```

> 💡 윈도우 함수는 기존 GROUP BY와 달리, 개별 행을 유지하면서 집계 가능.

---

### **4️⃣ 순위 함수 (Ranking Functions)**

| 함수 | 설명 | 동일 값 처리 |
|------|------|---------------|
| **RANK()** | 동일 값일 경우 다음 순위 건너뜀 | O |
| **DENSE_RANK()** | 동일 값 순위 유지 | X |
| **ROW_NUMBER()** | 단순 행 번호 부여 | - |

```sql
SELECT ename, sal,
       RANK() OVER (ORDER BY sal DESC) AS rank_no,
       DENSE_RANK() OVER (ORDER BY sal DESC) AS dense_no,
       ROW_NUMBER() OVER (ORDER BY sal DESC) AS row_no
FROM emp;
```

> ⚙️ 동일 급여자 처리 시, RANK와 DENSE_RANK의 차이에 주의.

---

## **⚙️ 모델링 유의사항**

1. GROUPING SETS / ROLLUP / CUBE는 대량 데이터에서 **성능 부하**가 큼  
2. CUBE는 가능한 모든 조합을 계산하므로 데이터 폭증 가능성 주의  
3. 윈도우 함수는 WHERE 절보다 **SELECT 이후 단계에서 실행**됨  
4. 순위 함수 사용 시 PARTITION 기준과 ORDER 기준을 명확히 지정  
5. ROLLUP, CUBE 결과를 외부 애플리케이션에서 가공 시 **NULL 처리 기준 통일 필요**

---

## **⚙️ 핵심 요약**

- GROUPING SETS, ROLLUP, CUBE는 데이터 분석용 다차원 요약 기능  
- GROUPING() 함수는 요약행 구분용 플래그 역할  
- 윈도우 함수는 개별 행 단위로 집계를 수행  
- RANK / DENSE_RANK / ROW_NUMBER는 순위 계산 시 자주 비교됨

---

## **🧮 예제 및 실습**

**예제 1️⃣ – GROUPING 확장 예시**
```sql
SELECT deptno, job, SUM(sal)
FROM emp
GROUP BY ROLLUP (deptno, job);
```

**예제 2️⃣ – GROUPING() 함수 적용**
```sql
SELECT deptno, job, SUM(sal),
       GROUPING(deptno) AS g_dept,
       GROUPING(job) AS g_job
FROM emp
GROUP BY ROLLUP (deptno, job);
```

**예제 3️⃣ – 윈도우 함수 실습**
```sql
SELECT deptno, ename, sal,
       RANK() OVER (PARTITION BY deptno ORDER BY sal DESC) AS rank_no
FROM emp;
```

- [x] GROUPING SETS / ROLLUP / CUBE 차이 실습  
- [x] GROUPING() 함수로 요약행 구분  
- [x] RANK, DENSE_RANK, ROW_NUMBER 비교  

---

## **🧾 기출 복습**

| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2024 2회 | Q71–Q75 | ROLLUP / CUBE 함수 | ✅ | 다차원 요약 구문 구분 |
| 2023 1회 | Q66–Q70 | 윈도우 함수 | ⚠ | PARTITION BY 생략 시 전체 집계됨 |
| 2022 2회 | Q61–Q65 | 순위 함수 비교 | ✅ | RANK vs DENSE_RANK 차이 |

> 📘 기출 출처: SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ **기출예상문제 2-13절~2-14절 (p.215~228)** 기반 정리

---

## **💬 느낀점 / 메모**

- GROUP BY 확장 문법은 단순 집계를 넘어 다차원 분석으로 가는 핵심이다.  
- 윈도우 함수는 데이터 분석 실무에서 거의 모든 통계 SQL의 기본 구성요소임을 체감했다.  
- RANK 계열 함수는 실무 보고서나 순위 데이터 처리에서 매우 자주 사용될 듯하다.

---

## **🔗 참고자료**

- 아이리포 SQLD 강의 – 2과목 21~23강 (유튜브 21~23강): GROUPING 및 윈도우 함수  
- SQLD 공식 교재 2권 p.215~228 (윈도우 함수)  
- [윈도우 함수 완전 정리 – SQLGate 블로그](https://www.sqlgate.com/blog/sql-window-functions)
