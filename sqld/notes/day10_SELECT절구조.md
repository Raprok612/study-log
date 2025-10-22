# SQLD Day 10 – SELECT / FROM / WHERE 절 구조 (2025-10-22)
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- SQL 문장의 기본 구조(SELECT-FROM-WHERE) 이해  
- 실행 순서와 필터링 조건의 처리 방식 숙지  
- 비교 연산자, 논리 연산자, BETWEEN / IN / LIKE 구문 익히기

---

## 🧠 이론 정리

### 1️⃣ SQL 문장의 기본 구조
```sql
SELECT [컬럼 목록]
FROM [테이블명]
WHERE [조건식];
```

| 절 | 설명 | 실행 순서 |
|----|------|------------|
| **FROM** | 데이터를 가져올 테이블 지정 | 1 |
| **WHERE** | 행(Row) 단위 조건 필터링 | 2 |
| **SELECT** | 최종 출력 컬럼 지정 | 3 |

> 💡 **실행 순서 핵심:** FROM → WHERE → SELECT  

---

### 2️⃣ WHERE 절 비교 / 논리 연산자
| 연산자 | 설명 | 예시 |
|---------|------|------|
| =, <>, >, <, >=, <= | 비교 연산 | sal > 3000 |
| BETWEEN A AND B | 구간 비교 | sal BETWEEN 2000 AND 5000 |
| IN (list) | 목록 비교 | deptno IN (10,20,30) |
| LIKE | 패턴 매칭 | ename LIKE 'S%' |
| IS NULL / IS NOT NULL | NULL 검사 | comm IS NULL |
| AND / OR / NOT | 논리 연산 | deptno=10 AND job='CLERK' |

---

### 3️⃣ 실행 예제
```sql
SELECT ename, job, sal
FROM emp
WHERE sal BETWEEN 2000 AND 5000
  AND job IN ('MANAGER', 'ANALYST');
```
- [x] WHERE 조건 실습  
- [x] LIKE / BETWEEN 비교 연습  
- [ ] NULL 포함 조건 추가 테스트  

---

## 🧾 기출 복습
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2023 2회 | Q41–Q45 | SELECT / WHERE 문법 | ✅ | |
| 2022 1회 | Q36–Q40 | SQL 실행 순서 | ⚠ | WHERE 절 처리 순서 복습 |

---

## 💬 느낀점 / 메모
- SQL 실행 순서(From→Where→Select)를 명확히 이해하니 쿼리 해석이 쉬워졌다.  
- WHERE절에서의 NULL 처리와 IN/LIKE 구문 결합 시 주의 필요.  
- SELECT문은 단순 조회가 아니라 “조건 기반 데이터 추출 절차”라는 점이 중요하다.

---

## 🔗 참고자료
- 아이리포 SQLD 강의 – 2과목 3강: SELECT / FROM / WHERE 문  
- SQLD 교재 2권 p.49~72  
- [SQL 기본 SELECT 문법 요약 – SQLGate 블로그](https://www.sqlgate.com/blog/sql-select-basics/)
