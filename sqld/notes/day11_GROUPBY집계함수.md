# **SQLD Day 11 – GROUP BY 절과 집계 함수 활용 (2025-10-23)**
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**
- GROUP BY 절의 역할과 작동 방식 이해  
- SUM, AVG, COUNT 등 집계 함수 사용법 숙지  
- GROUP BY와 HAVING 절의 차이점 이해

---

## **🧠 이론 정리**

### **1️⃣ GROUP BY의 개념**
> GROUP BY 절은 **데이터를 특정 기준으로 묶어 요약(집계)** 하는 데 사용된다.

```sql
SELECT deptno, AVG(sal)
FROM emp
GROUP BY deptno;
```

| 구문 요소 | 설명 |
|------------|------|
| **GROUP BY** | 특정 컬럼 기준으로 데이터 그룹화 |
| **HAVING** | 그룹화된 결과에 조건을 적용 |
| **집계 함수** | 그룹별 계산 수행 (SUM, AVG, COUNT 등) |

> 💡 WHERE는 그룹화 이전, HAVING은 그룹화 이후 조건을 적용한다.

---

### **2️⃣ 주요 집계 함수**
| 함수 | 설명 | 예시 |
|------|------|------|
| **COUNT(expr)** | 행의 개수 반환 | `COUNT(*)`, `COUNT(empno)` |
| **SUM(expr)** | 합계 계산 | `SUM(sal)` |
| **AVG(expr)** | 평균 계산 | `AVG(sal)` |
| **MAX(expr)** | 최대값 반환 | `MAX(sal)` |
| **MIN(expr)** | 최소값 반환 | `MIN(sal)` |

> ⚙️ NULL 값은 대부분의 집계 연산에서 제외된다.

---

### **3️⃣ GROUP BY + HAVING 예제**
```sql
SELECT deptno, AVG(sal) AS avg_sal
FROM emp
GROUP BY deptno
HAVING AVG(sal) > 2000
ORDER BY avg_sal DESC;
```

> 💡 HAVING 절은 **집계 결과에 조건**을 주는 유일한 절이다.

---

## **⚙️ 모델링 유의사항**
1. GROUP BY 컬럼은 SELECT 절에 반드시 포함되어야 함  
2. WHERE과 HAVING의 적용 시점을 혼동하지 말 것  
3. NULL 값 포함 여부에 따라 결과가 달라질 수 있음  

---

## **⚙️ 핵심 요약**
- GROUP BY는 데이터를 **요약·통계 처리**하기 위한 핵심 절이다.  
- HAVING은 그룹화된 결과를 필터링하며, WHERE과 구분되어야 한다.  
- COUNT(*), AVG, SUM 등 집계 함수는 NULL 제외 특성을 이해해야 한다.

---

## **🧮 예제 및 실습**
```sql
SELECT deptno, COUNT(*) AS cnt, SUM(sal) AS total_sal
FROM emp
GROUP BY deptno
HAVING SUM(sal) > 10000;
```
- [x] GROUP BY 기본 예제 실습  
- [x] HAVING 조건 적용 테스트  
- [ ] NULL 포함 여부 비교 실험  

---

## **🧾 기출 복습**
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2023 2회 | Q51–Q55 | GROUP BY와 HAVING 구분 | ✅ | HAVING은 그룹화 이후 조건 |
| 2022 1회 | Q46–Q50 | 집계 함수 사용 규칙 | ⚠ | NULL 포함시 결과 차이 확인 |

> 📘 **기출 출처:**  
> SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ **기출예상문제 2-5절 (p.147~155)** 기반 정리

---

## **💬 느낀점 / 메모**
- WHERE와 HAVING의 순서 차이를 직접 실습하니 개념이 명확해졌다.  
- COUNT(*)와 COUNT(column)의 차이는 실제 업무에서도 자주 실수하는 부분임을 깨달았다.  
- 그룹 함수의 NULL 처리 방식이 결과에 큰 영향을 준다는 점이 흥미로웠다.

---

## **🔗 참고자료**
- 아이리포 SQLD 강의 – 2과목 11강 (유튜브 11강): GROUP BY 절과 집계 함수  
- SQLD 공식 교재 2권 p.69~88, p.147~155 (기출예상문제)  
- [GROUP BY와 HAVING 구문 – SQLGate 블로그](https://www.sqlgate.com/blog/sql-groupby-having)
