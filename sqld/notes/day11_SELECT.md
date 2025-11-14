# **SQLD Day 11 – SELECT 절 구조 및 SQL 실행 순서 이해 (2025-10-23)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- SELECT 절의 기본 구조 이해  
- SQL 실행 순서(Execution Order) 완전 숙지  
- WHERE, GROUP BY, HAVING, ORDER BY의 동작 흐름 파악  

---

## 🧠 이론 정리

### 1️⃣ SELECT 문 기본 구조

```sql
SELECT 컬럼
FROM 테이블
WHERE 조건
GROUP BY 그룹기준
HAVING 그룹조건
ORDER BY 정렬기준;
```

---

### 2️⃣ SQL 실행 순서 (중요!)

| 실행 순서 | 키워드 | 설명 |
|---|---|---|
| **1** | FROM | 테이블 결정 |
| **2** | WHERE | 조건 필터링 |
| **3** | GROUP BY | 그룹 생성 |
| **4** | HAVING | 그룹 조건 필터링 |
| **5** | SELECT | 컬럼 출력 |
| **6** | ORDER BY | 결과 정렬 |

> 💡 SELECT가 5번째라는 점이 핵심!  
> 계산식, 별칭(alias) 사용 가능 여부가 순서에 따라 달라진다.

---

### 3️⃣ 별칭(Alias) 사용 규칙

| 위치 | 별칭 사용 가능 여부 |
|---|---|
| SELECT | 가능 |
| ORDER BY | 가능 |
| WHERE | ❌ 불가능 (SELECT보다 먼저 실행) |
| HAVING | 가능 |

---

## ⚙️ 핵심 요약
- SQL 실행 순서를 정확히 이해하면 문제풀이 속도와 정확도가 크게 향상된다.  
- WHERE과 HAVING의 차이는 실행 순서에서 비롯된다.  
- SELECT는 5번째—이것 때문에 WHERE에서 별칭을 못 쓴다.

---

## 🧮 실습 예제

```sql
SELECT deptno, AVG(sal) AS avg_sal
FROM emp
WHERE sal > 1000
GROUP BY deptno
HAVING AVG(sal) >= 2000
ORDER BY avg_sal DESC;
```

---

## 💬 느낀점
- 실행 순서를 알고 나니 SELECT 구문의 작동 방식이 훨씬 명확해졌다.  
- WHERE과 HAVING의 차이를 헷갈리지 않을 자신이 생겼다.  
- 문제 풀이에서 조건과 그룹 순서를 다시 점검하게 되었다.

---

## 🔗 참고자료
- 아이리포 SQLD 강의 – 2과목 11강  
- SQLD 공식 교재 2권 p.56~76
