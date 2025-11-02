# **SQLD Day 21 – 기출 유형 정리, 실전 응용 쿼리 분석 (2025-11-02)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**

- SQLD 과거 기출 유형별 핵심 패턴 정리  
- 실전형 복합 쿼리(서브쿼리, 윈도우 함수, PIVOT) 분석  
- SQL 문장 해석력 및 문제 해결 논리 강화

---

## **🧠 이론 정리**

### **1️⃣ SQLD 기출 출제 경향 요약**

| 구분 | 출제 비중 | 핵심 개념 |
|------|------------|------------|
| 데이터 모델링 | 약 30% | 엔터티, 관계, 식별자, 정규화 |
| SQL 기본문 | 약 40% | SELECT, JOIN, GROUP BY, 서브쿼리 |
| SQL 고급문 | 약 20% | 윈도우 함수, PIVOT, RANK |
| 기타 | 약 10% | NULL, 트랜잭션, 무결성 제약 |

> 💡 SQL 문법 중심으로 2과목(SELECT~JOIN) 영역이 가장 높은 비중을 차지함.

---

### **2️⃣ 자주 등장하는 쿼리 패턴**

| 유형 | 예시 | 핵심 포인트 |
|------|------|--------------|
| **JOIN** | INNER / LEFT / SELF | ON 절 조건 중요, NULL 처리 유의 |
| **서브쿼리** | EXISTS / IN / ANY / ALL | 다중행 비교, 조건 내 SELECT |
| **집계함수** | ROLLUP / CUBE / GROUPING | NULL 그룹 처리 및 결과 차이 |
| **윈도우함수** | RANK / DENSE_RANK / ROW_NUMBER | 순위 중복 및 PARTITION 차이 |
| **문자열 처리** | SUBSTR / REPLACE / NVL / COALESCE | 공백 및 NULL 대응 |

> ⚙️ 기출에서는 위 함수들이 복합적으로 결합된 형태로 자주 등장함.

---

## **⚙️ 실전 분석 포인트**

1. **조건 해석력**: 문제의 “최대”, “상위 N건”, “포함되지 않는” 등의 문구를 SQL로 변환  
2. **그룹 단위 사고**: 단일행 vs 다중행 쿼리 구분 능력  
3. **JOIN 방향성 이해**: INNER / OUTER 결과 차이 인식  
4. **NULL 처리 감각**: NVL, COALESCE, ISNULL의 차이를 빠르게 구분  

---

## **🧮 예제 및 실습**

**예제 1️⃣ – 다중 JOIN + 집계 조합 문제**
```sql
SELECT D.DEPT_NAME, COUNT(E.EMP_ID) AS CNT, SUM(E.SAL) AS TOTAL_SAL
FROM DEPT D
LEFT JOIN EMP E ON D.DEPT_ID = E.DEPT_ID
GROUP BY D.DEPT_NAME
HAVING SUM(E.SAL) > 10000
ORDER BY TOTAL_SAL DESC;
```

**예제 2️⃣ – 서브쿼리 응용**
```sql
SELECT NAME, SAL
FROM EMP
WHERE SAL > (SELECT AVG(SAL) FROM EMP);
```

**예제 3️⃣ – 윈도우 함수 응용**
```sql
SELECT DEPTNO, ENAME, SAL,
       RANK() OVER (PARTITION BY DEPTNO ORDER BY SAL DESC) AS RANK_SAL
FROM EMP;
```

- [x] JOIN과 GROUP BY 조합 문제 풀이  
- [x] 서브쿼리 평균 비교 실습  
- [x] 윈도우 함수 순위 정렬 실습

---

## **🧾 기출 복습**

| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2024 2회 | Q61–Q65 | JOIN 및 서브쿼리 결합 | ✅ | 조건 해석 정확 |
| 2023 1회 | Q56–Q60 | 윈도우 함수 RANK / DENSE_RANK | ⚠ | PARTITION 구분 주의 |
| 2022 2회 | Q51–Q55 | GROUP BY + HAVING | ✅ | NULL 그룹 결과 해석 |

> 📘 기출 출처: SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ 기출예상문제 2-19절~2-20절 (p.261~274)

---

## **💬 느낀점 / 메모**

- 복합 쿼리 문제에서는 **실행 순서**(FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY)의 흐름이 핵심이다.  
- 서브쿼리와 윈도우 함수가 결합된 문제는 순서·스코프를 정확히 구분해야 한다.  
- 실제 기출을 풀면서 쿼리 결과를 예측하는 능력이 점점 향상됨을 체감했다.

---

## **🔗 참고자료**

- 아이리포 SQLD 강의 – 2과목 34~37강 (유튜브 34~37강): 기출 유형 정리 / 실전 응용 쿼리 분석  
- SQLD 공식 교재 2권 p.261~274  
- [아이리포 공식 유튜브 채널 – SQLD 모든 것](https://www.youtube.com/@irepo_official)
