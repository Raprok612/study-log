# **SQLD Day 12 – JOIN의 개념과 종류 (2025-10-24)**
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**
- JOIN의 개념과 필요성 이해  
- INNER / OUTER / CROSS JOIN의 차이 구분  
- ON / USING / NATURAL JOIN 구문 숙지

---

## **🧠 이론 정리**

### **1️⃣ JOIN의 개념**
> 두 개 이상의 테이블을 **공통 컬럼을 기준으로 결합**하여 데이터를 조회하는 SQL 연산이다.

| 구분 | 설명 | 예시 |
|------|------|------|
| **INNER JOIN** | 두 테이블에서 조건을 만족하는 행만 반환 | `SELECT * FROM A INNER JOIN B ON A.id = B.id;` |
| **LEFT OUTER JOIN** | 왼쪽 테이블의 모든 행 + 일치하는 오른쪽 행 | `SELECT * FROM A LEFT OUTER JOIN B ON A.id = B.id;` |
| **RIGHT OUTER JOIN** | 오른쪽 테이블의 모든 행 + 일치하는 왼쪽 행 | `SELECT * FROM A RIGHT OUTER JOIN B ON A.id = B.id;` |
| **FULL OUTER JOIN** | 양쪽 테이블의 모든 행 반환 (NULL 포함) | `SELECT * FROM A FULL OUTER JOIN B ON A.id = B.id;` |
| **CROSS JOIN** | 모든 행의 조합(곱집합) 반환 | `SELECT * FROM A, B;` |

> 💡 OUTER JOIN은 **한쪽 데이터가 없더라도 결과에 포함된다는 점**이 핵심이다.

---

### **2️⃣ JOIN 조건 구문**
| 구문 | 특징 | 예시 |
|------|------|------|
| **ON** | 일반적인 조인 조건 명시 | `A JOIN B ON A.id = B.id` |
| **USING** | 공통 컬럼명이 동일할 때 간결하게 사용 | `A JOIN B USING (id)` |
| **NATURAL JOIN** | 공통 컬럼을 자동으로 인식하여 조인 | `A NATURAL JOIN B` |

> ⚙️ USING과 NATURAL JOIN은 컬럼명이 동일해야 하며, **명시적 제어가 어렵다.**

---

### **3️⃣ 실무에서 자주 쓰이는 JOIN 패턴**
- **SELF JOIN:** 동일 테이블 내에서 자기 자신과 조인  
- **NON-EQUI JOIN:** 부등호(>, <) 조건을 사용하는 조인  
- **THETA JOIN:** 일반적인 비교 연산자를 사용하는 조인  

```sql
SELECT e.ename, m.ename AS manager
FROM emp e
JOIN emp m ON e.mgr = m.empno;
```

---

## **⚙️ 모델링 유의사항**
1. 조인 조건이 없으면 **CARTESIAN PRODUCT(곱집합)** 발생  
2. JOIN 시 인덱스 사용 여부와 실행 계획(Execution Plan)을 반드시 검토  
3. NATURAL JOIN은 자동 매핑으로 인해 **명시적 제어 어려움** → 실무에서는 지양

---

## **⚙️ 핵심 요약**
- JOIN은 다중 테이블 간의 관계를 기반으로 데이터를 결합하는 핵심 SQL 기능이다.  
- INNER JOIN은 교집합, OUTER JOIN은 합집합 개념과 유사하다.  
- 실무에서는 ON 절을 통한 명시적 조인 조건 설정이 표준이다.

---

## **🧮 예제 및 실습**
```sql
SELECT e.ename, d.dname
FROM emp e
JOIN dept d ON e.deptno = d.deptno;
```
- [x] INNER JOIN 실습  
- [x] LEFT / RIGHT JOIN 비교  
- [ ] FULL OUTER JOIN 실습 (DBMS별 차이 확인)

---

## **🧾 기출 복습**
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2023 2회 | Q56–Q60 | JOIN 종류 구분 | ✅ | INNER / OUTER / CROSS 구분 확인 |
| 2022 1회 | Q51–Q55 | NATURAL JOIN, USING 문법 | ⚠ | USING 컬럼명 중복 주의 |

> 📘 **기출 출처:**  
> SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ **기출예상문제 2-6절 (p.156~165)** 기반 정리

---

## **💬 느낀점 / 메모**
- INNER JOIN과 OUTER JOIN의 차이를 시각적으로 정리하니 개념이 명확해졌다.  
- 실무에서는 NATURAL JOIN보다 ON 조건 기반 조인을 선호하는 이유를 이해했다.  
- JOIN 조건을 명시적으로 관리하는 것이 SQL 가독성과 유지보수성을 높인다.

---

## **🔗 참고자료**
- 아이리포 SQLD 강의 – 2과목 12강 (유튜브 12강): JOIN의 개념과 종류  
- SQLD 공식 교재 2권 p.89~108, p.156~165 (기출예상문제)  
- [SQL JOIN 종류 정리 – SQLGate 블로그](https://www.sqlgate.com/blog/sql-join-types)
