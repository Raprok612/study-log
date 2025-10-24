# SQLD Day 12 – JOIN의 개념과 종류 (2025-10-24)
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- JOIN의 개념과 필요성 이해  
- INNER / OUTER / CROSS JOIN의 차이 숙지  
- ON / USING / NATURAL JOIN 구문 학습

---

## 🧠 이론 정리

### 1️⃣ JOIN의 개념
> 두 개 이상의 테이블을 연결하여 관련 데이터를 조회하는 SQL 연산

- 기본적으로 **공통 컬럼(키)** 을 기준으로 연결  
- 조인 조건이 없으면 **CARTESIAN PRODUCT (곱집합)** 발생

```sql
SELECT e.ename, d.dname
FROM emp e, dept d
WHERE e.deptno = d.deptno;
```

---

### 2️⃣ JOIN의 종류

| 구분 | 설명 | 예시 |
|------|------|------|
| **INNER JOIN** | 두 테이블에서 조건을 만족하는 행만 | `SELECT * FROM A INNER JOIN B ON A.id=B.id;` |
| **LEFT OUTER JOIN** | 왼쪽 테이블의 모든 행 + 일치하는 오른쪽 행 | `SELECT * FROM A LEFT OUTER JOIN B ON A.id=B.id;` |
| **RIGHT OUTER JOIN** | 오른쪽 테이블의 모든 행 + 일치하는 왼쪽 행 | `SELECT * FROM A RIGHT OUTER JOIN B ON A.id=B.id;` |
| **FULL OUTER JOIN** | 양쪽 모든 행 (NULL 포함) | `SELECT * FROM A FULL OUTER JOIN B ON A.id=B.id;` |
| **CROSS JOIN** | 모든 조합 (곱집합) | `SELECT * FROM A, B;` |

> 💡 OUTER JOIN은 **한쪽 테이블의 데이터가 없어도 표시**된다는 점이 핵심

---

### 3️⃣ JOIN 조건 구문
| 구문 | 특징 | 예시 |
|------|------|------|
| **ON** | 일반 조인 조건 명시 | `A JOIN B ON A.id=B.id` |
| **USING** | 공통 컬럼 이름이 동일할 때 | `A JOIN B USING (id)` |
| **NATURAL JOIN** | 공통 컬럼 자동 인식 | `A NATURAL JOIN B` |

---

## 🧮 예제 및 실습

```sql
SELECT e.ename, d.dname
FROM emp e
JOIN dept d
ON e.deptno = d.deptno;
```

- [x] INNER JOIN 실습  
- [x] LEFT / RIGHT JOIN 비교  
- [ ] FULL OUTER JOIN 실습 (DBMS 별 차이 확인)

---

## 🧾 기출 복습
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2023 2회 | Q51–Q55 | JOIN 종류 구분 | ✅ | |
| 2022 1회 | Q46–Q50 | OUTER JOIN / NATURAL JOIN | ⚠ | DBMS별 차이 확인 필요 |

---

## 💬 느낀점 / 메모
- JOIN은 데이터베이스 관계 모델의 핵심 구현 구조.  
- INNER JOIN은 교집합, OUTER JOIN은 합집합 개념과 유사하다.  
- JOIN 조건을 WHERE절에 두면 가독성이 떨어지므로 `ON` 구문 사용이 표준 SQL 스타일이다.

---

## 🔗 참고자료
- 아이리포 SQLD 강의 – 2과목 5강: JOIN 개념 및 종류  
- SQLD 교재 2권 p.95~118  
- [SQL JOIN 종류 정리 – SQLGate 블로그](https://www.sqlgate.com/blog/sql-join-types/)
