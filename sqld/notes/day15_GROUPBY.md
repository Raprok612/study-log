# **SQLD Day 15 – GROUP BY 절 (2025-10-27)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**

- GROUP BY 절의 동작 원리 이해  
- 집계 함수와 함께 사용하는 다양한 패턴 학습  
- HAVING 절의 역할과 WHERE와의 차이 구분  

---

## **🧠 이론 정리**

### 1️⃣ GROUP BY의 개념

> 행(Row)을 특정 기준으로 묶어(Grouping) 집계 연산을 수행하는 절.

| 구성 | 설명 |
|-----|------|
| **GROUP BY** | 데이터를 그룹 단위로 묶음 |
| **집계 함수** | SUM, AVG, MAX, MIN, COUNT |
| **HAVING** | 그룹핑된 결과에 조건 적용 |

---

### 2️⃣ GROUP BY 사용 시 주의사항

- SELECT 절에 오는 일반 컬럼은 반드시 **GROUP BY**에 포함되어야 한다  
- WHERE → GROUP BY → HAVING → ORDER BY 순으로 처리  
- HAVING은 **GROUP BY 이후 필터링**, WHERE는 **GROUP BY 이전 필터링**

---

### 3️⃣ 예제

```sql
SELECT deptno, AVG(sal)
FROM emp
GROUP BY deptno;
```

```sql
SELECT deptno, AVG(sal)
FROM emp
WHERE sal > 1000
GROUP BY deptno
HAVING AVG(sal) > 2000;
```

---

## **⚙️ 핵심 요약**

- GROUP BY는 데이터를 묶어 집계하는 SQL의 핵심 기능  
- WHERE는 그룹화 전 조건, HAVING은 그룹화 후 조건  
- SELECT 절에서 집계되지 않은 컬럼은 반드시 GROUP BY에 포함  

---

## **💬 느낀점 / 메모**

- WHERE와 HAVING의 차이를 실제 실행 순서와 함께 이해하니 훨씬 명확해졌다.  
- GROUP BY는 실무에서도 자주 사용되기 때문에 반드시 손에 익혀야 한다.  

---

## **🔗 참고자료**

- 아이리포 SQLD 강의 – 2과목 15강  
- SQLD 공식 교재 2권 p.145~160
