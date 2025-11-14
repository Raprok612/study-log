# **SQLD Day 10 – 관계형 데이터베이스 구조 이해 (2025-10-22)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- 관계형 데이터베이스의 기본 구조와 개념 이해  
- 릴레이션(Relation), 튜플(Tuple), 속성(Attribute) 개념 정리  
- 키(Key) 종류 및 제약조건(Constraints) 이해  

---

## 🧠 이론 정리

### 1️⃣ 관계형 데이터베이스의 구성 요소

| 용어 | 설명 | 예시 |
|---|---|---|
| **릴레이션(Relation)** | 테이블 | EMP, DEPT |
| **튜플(Tuple)** | 테이블의 한 행(Row) | 사원 정보 한 줄 |
| **속성(Attribute)** | 테이블의 컬럼(Column) | EMPNO, SAL |
| **도메인(Domain)** | 속성이 가질 수 있는 값의 범위 | SAL → NUMBER(7,2) |

---

### 2️⃣ 키(Key)의 종류 요약

| 키 종류 | 설명 | 특징 |
|---|---|---|
| **후보키(Candidate Key)** | 기본키가 될 수 있는 후보 | 유일성 + 최소성 |
| **기본키(Primary Key)** | 테이블의 대표 식별자 | 중복·NULL 불가 |
| **대체키(Alternate Key)** | 후보키 중 기본키로 선택되지 않은 키 | 유일성 유지 |
| **외래키(Foreign Key)** | 다른 테이블의 기본키 참조 | 참조무결성 |
| **슈퍼키(Super Key)** | 유일성만 만족하는 키 | 최소성 불필요 |

---

### 3️⃣ 제약조건(Constraints)

| 제약조건 | 의미 |
|---|---|
| **NOT NULL** | NULL 금지 |
| **UNIQUE** | 중복 금지 |
| **PRIMARY KEY** | NOT NULL + UNIQUE |
| **FOREIGN KEY** | 참조 무결성 |
| **CHECK** | 값의 조건 지정 |
| **DEFAULT** | 기본값 설정 |

---

## ⚙️ 핵심 요약
- 관계형 데이터베이스는 릴레이션 기반 구조이며, 행과 열로 구성된다.  
- 키(Key)는 데이터를 식별하고 무결성을 유지하는 핵심 요소이다.  
- 제약조건은 데이터 정확성과 일관성을 보장하는 장치이다.

---

## 🧮 실습 예제

```sql
CREATE TABLE EMP (
    EMPNO NUMBER PRIMARY KEY,
    ENAME VARCHAR2(20) NOT NULL,
    DEPTNO NUMBER,
    CONSTRAINT fk_dept FOREIGN KEY (DEPTNO)
        REFERENCES DEPT(DEPTNO)
);
```

---

## 💬 느낀점
- 관계형 데이터베이스 구조는 SQL의 모든 개념의 기반이 된다.  
- 키와 제약조건을 확실히 이해하면 ERD 해석 및 문제 풀이 속도가 빨라진다.  
- 실제 업무 DB 구조와 비교하며 학습하니 이해가 더 깊어졌다.

---

## 🔗 참고자료
- 아이리포 SQLD 강의 – 2과목 10강  
- SQLD 공식 교재 2권 p.30~55
