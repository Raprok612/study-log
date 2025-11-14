# **SQLD Day 14 – WHERE절 조건 처리 및 비교 연산 (2025-10-26)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- WHERE절의 평가 순서 및 조건 최적화 이해  
- 비교 연산자, 논리 연산자 우선순위 숙지  
- NULL 비교 관련 함정 정리  

---

## 🧠 이론 정리

### 1️⃣ WHERE절의 역할
> **조건에 맞는 행(Row)을 필터링하는 단계**  
SQL 실행 순서:  
FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY

---

### 2️⃣ 비교 연산자 정리
| 연산자 | 의미 | 예시 |
|-------|------|------|
| = | 같음 | deptno = 10 |
| !=, <> | 같지 않음 | sal <> 3000 |
| >, <, >=, <= | 비교 | sal > 2000 |
| BETWEEN A AND B | A~B 포함 | sal BETWEEN 1000 AND 2000 |
| IN (list) | 여러 값 중 하나 | job IN ('MANAGER','CLERK') |
| LIKE | 패턴 검색 | ename LIKE 'S%' |

---

### 3️⃣ 논리 연산자 우선순위
우선순위:  
1. **NOT**  
2. **AND**  
3. **OR**

```sql
WHERE NOT (A = 10 OR B = 20)
```

---

### 4️⃣ NULL 비교 주의사항
- `col = NULL` → ❌ 언제나 FALSE  
- 반드시 `IS NULL` / `IS NOT NULL`

GROUP 함수 특징:
- SUM, AVG, MIN, MAX는 NULL 제외
- COUNT(col) → NULL 제외
- COUNT(*) → 모든 행 포함

---

## 🧮 실습

```sql
SELECT empno, ename, sal
FROM emp
WHERE sal BETWEEN 2000 AND 4000
  AND job IN ('MANAGER','ANALYST');
```

- [x] WHERE절 필터링 실습  
- [x] 논리 연산자 우선순위 비교  
- [ ] LIKE 패턴 실습 추가 예정  

---

## ⚙️ 핵심 요약
- WHERE절은 조건 필터링 단계이며 SQL 실행 순서에서 매우 중요  
- AND가 OR보다 우선순위가 높음  
- NULL 비교는 항상 IS NULL로 수행  

---

## 💬 느낀점
- WHERE절을 정확히 이해하면 SQL의 60%는 잡는다고 느꼈다.  
- 실제 업무에서 조건 조합이 많을수록 우선순위 오류가 자주 발생하기 때문에 주의가 필요함.  

---

## 🔗 참고자료
- 아이리포 SQLD 14강 – WHERE절  
- SQLD 공식 교재 2권 p.140~149
