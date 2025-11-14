# **SQLD Day 16 – 조인(JOIN) 핵심 정리 (2025-10-28)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**
- INNER / OUTER / CROSS JOIN 구조 이해  
- LEFT JOIN vs WHERE 조건 위치별 결과 차이 파악  
- JOIN 조건의 실행 순서 및 필터링 로직 학습  
- 시험에서 자주 나오는 JOIN 함정 포인트 정리

---

## **🧠 이론 정리**

### **1️⃣ JOIN의 기본 개념**
두 테이블을 연결하여 데이터를 결합하는 방식.

| JOIN 유형 | 설명 | 특징 |
|----------|------|-------|
| **INNER JOIN** | 교집합 | 매칭되는 행만 반환 |
| **LEFT OUTER JOIN** | 왼쪽 기준 모든 행 + 오른쪽 매칭 | 오른쪽 없는 값은 NULL |
| **RIGHT OUTER JOIN** | 오른쪽 기준 모든 행 | 일반적으로 잘 쓰이지 않음 |
| **FULL OUTER JOIN** | 양쪽 모두 포함 | ORACLE은 SQL 표준 FULL OUTER JOIN만 지원 |
| **CROSS JOIN** | 모든 조합 생성 | 카테시안 곱 |

---

## **2️⃣ JOIN 핵심 규칙**

### ✔ INNER JOIN
```sql
SELECT *
FROM A
INNER JOIN B ON A.id = B.id;
```

---

### ✔ LEFT OUTER JOIN (시험 단골 함정)
```sql
SELECT *
FROM A
LEFT JOIN B ON A.id = B.id;
```

**⚠ WHERE 절에 B 조건을 넣으면 INNER JOIN처럼 동작**

```sql
SELECT *
FROM A
LEFT JOIN B ON A.id = B.id
WHERE B.score > 80;   -- ❌ LEFT JOIN 유지되지 않음
```

**정답 패턴**
```sql
SELECT *
FROM A
LEFT JOIN B ON A.id = B.id AND B.score > 80;
```

---

### **3️⃣ ANSI JOIN vs ORACLE JOIN**
| 방식 | 예시 |
|------|------|
| ANSI 표준 | `A LEFT JOIN B ON ...` |
| ORACLE 구문 | `A.column = B.column(+)` |

---

### **4️⃣ CROSS JOIN (카테시안 곱)**
```sql
SELECT *
FROM A
CROSS JOIN B;
```

---

## **🧮 예제 및 실습**

### ✔ LEFT JOIN 실전
```sql
SELECT D.deptno, D.dname, E.ename
FROM dept D
LEFT JOIN emp E ON D.deptno = E.deptno
WHERE E.ename IS NULL;
```

### ✔ INNER JOIN 예제
```sql
SELECT E.ename, D.dname
FROM emp E
JOIN dept D ON E.deptno = D.deptno;
```

### ✔ CROSS JOIN 예제
```sql
SELECT *
FROM dept CROSS JOIN emp;
```

---

## **⚙️ 핵심 요약**
- OUTER JOIN의 조건 위치는 시험 최다 함정  
- WHERE 절의 조건은 JOIN 이후 필터링  
- LEFT JOIN 조건은 반드시 **ON 절에 작성**  
- CROSS JOIN은 모든 조합 → 조심  
- SQLD는 ANSI JOIN 기준 출제  

---

## **🧾 기출 복습**
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 기출 2회 | Q41–Q45 | JOIN 유형 | ✅ | OUTER JOIN 필터링 |
| 기출 3회 | Q31–Q35 | ANSI JOIN | ⚠ | WHERE vs ON 차이 |

---

## **💬 느낀점**
- LEFT JOIN의 조건 실수 하나로 결과가 뒤집히는 경험을 다시 확인했다.  
- JOIN은 출제비중이 높기 때문에 완전한 이해가 필수다.  
- “JOIN은 실행 순서가 곧 정답이다”라는 말을 실감했다.

---

## **🔗 참고자료**
- 아이리포 SQLD 강의 – 2과목 16강: 조인(JOIN)  
- SQLD 공식 교재 2권 p.150~165  
