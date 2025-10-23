# SQLD Day 11 – GROUP BY 절 및 집계함수 (2025-10-23)
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- GROUP BY 절의 역할과 집계 기준 이해  
- 집계 함수(SUM, AVG, COUNT, MAX, MIN) 사용법 숙지  
- ROLLUP / CUBE / GROUPINGSETS 개념 파악

---

## 🧠 이론 정리

### 1️⃣ GROUP BY 절의 개념
- 동일한 값을 갖는 행(Row)을 그룹화하여 **집계(aggregation)** 수행  
- SELECT문에 집계함수를 포함할 때 **GROUP BY 필수**

```sql
SELECT deptno, AVG(sal)
FROM emp
GROUP BY deptno;
```

| 절 | 실행 순서 | 설명 |
|----|------------|------|
| FROM | 1 | 데이터 원천 지정 |
| WHERE | 2 | 조건 필터링 |
| GROUP BY | 3 | 그룹화 수행 |
| HAVING | 4 | 그룹 조건 |
| SELECT | 5 | 최종 컬럼 선택 |

---

### 2️⃣ 집계 함수 요약

| 함수 | 설명 | 예시 |
|------|------|------|
| **SUM(expr)** | 합계 | SUM(sal) |
| **AVG(expr)** | 평균 | AVG(sal) |
| **COUNT(expr)** | 행 수 | COUNT(*) |
| **MAX(expr)** | 최댓값 | MAX(sal) |
| **MIN(expr)** | 최솟값 | MIN(sal) |

> ⚠️ **NULL은 집계에서 제외됨**

---

### 3️⃣ ROLLUP / CUBE / GROUPINGSETS
| 함수 | 설명 | 예시 |
|------|------|------|
| **ROLLUP** | 상위 수준까지 누적합 | `GROUP BY ROLLUP(deptno, job)` |
| **CUBE** | 모든 조합에 대한 집계 | `GROUP BY CUBE(deptno, job)` |
| **GROUPINGSETS** | 특정 그룹 조합만 집계 | `GROUP BY GROUPING SETS((deptno), (job))` |

> 💡 ROLLUP → 부분합,  
> CUBE → 전체 조합,  
> GROUPINGSETS → 맞춤 조합.

---

### 4️⃣ HAVING 절
- GROUP BY 결과에 조건을 추가할 때 사용
```sql
SELECT deptno, AVG(sal)
FROM emp
GROUP BY deptno
HAVING AVG(sal) > 3000;
```

---

## 🧾 기출 복습
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2023 2회 | Q46–Q50 | GROUP BY / HAVING / ROLLUP | ✅ | |
| 2022 1회 | Q41–Q45 | 집계함수 / 그룹화 | ⚠ | ROLLUP, CUBE 구분 복습 필요 |

---

## 💬 느낀점 / 메모
- GROUP BY는 데이터 요약의 핵심이며, WHERE보다 늦게 실행된다는 점 중요.  
- ROLLUP과 CUBE는 실무에서도 자주 등장하지 않지만, SQLD에서는 자주 출제됨.  
- HAVING은 GROUP 결과 필터링용임을 기억하자.

---

## 🔗 참고자료
- 아이리포 SQLD 강의 – 2과목 4강: GROUP BY / 집계함수  
- SQLD 교재 2권 p.73~94  
- [GROUP BY 절과 ROLLUP / CUBE 요약 – SQLGate 블로그](https://www.sqlgate.com/blog/sql-groupby-rollup/)
