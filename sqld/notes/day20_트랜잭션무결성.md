# SQLD Day 20 – 트랜잭션 / 무결성 / DDL·DML 종합 복습 (2025-11-01)

> 날짜: 2025-11-01  
> 학습자: Jaerok Kim (Raprok612)  
> 강의: 30~33강  
> 주제: 트랜잭션 / 무결성 / DDL·DML 종합 복습  

---

## 🎯 학습 목표

- 트랜잭션(Transaction)의 개념 및 특성(ACID) 이해
- 무결성 제약조건의 종류 및 역할 숙지
- DDL, DML, DCL 문법을 비교·정리하고 실무형 예제 복습
- SQL 문장 실행 순서 및 트랜잭션 제어 로직 정리

---

## 🧠 이론 정리

### 🔹 1. 트랜잭션(Transaction)

> 데이터베이스의 **논리적 작업 단위**로, 모든 연산이 완전하게 수행되어야 함.

| 속성 | 설명 |
|------|------|
| **A (Atomicity)** | 원자성 – 전부 수행되거나 전혀 수행되지 않음 |
| **C (Consistency)** | 일관성 – 트랜잭션 전후 데이터 무결성 유지 |
| **I (Isolation)** | 고립성 – 동시에 실행되는 트랜잭션 간 간섭 방지 |
| **D (Durability)** | 지속성 – 커밋된 데이터는 영구 반영 |

```sql
BEGIN TRANSACTION;
UPDATE ACCOUNT SET BALANCE = BALANCE - 1000 WHERE ID = 'A';
UPDATE ACCOUNT SET BALANCE = BALANCE + 1000 WHERE ID = 'B';
COMMIT;
```

> ⚠️ 하나라도 실패 시 ROLLBACK으로 복원

---

### 🔹 2. 무결성 제약조건

| 제약조건 | 설명 | 예시 |
|-----------|--------|------|
| **PRIMARY KEY** | 엔터티의 고유 식별자 | `PRIMARY KEY (EMP_ID)` |
| **FOREIGN KEY** | 다른 테이블의 기본키 참조 | `FOREIGN KEY (DEPT_ID) REFERENCES DEPT(DEPT_ID)` |
| **UNIQUE** | 중복 불허 | `UNIQUE (EMAIL)` |
| **NOT NULL** | NULL 불허 | `NOT NULL` |
| **CHECK** | 조건식 검증 | `CHECK (AGE >= 18)` |

> 💡 제약조건은 데이터 무결성을 보장하는 핵심 장치이며,  
> 트랜잭션 실패 시 데이터 불일치를 방지.

---

### 🔹 3. DDL / DML / DCL 비교

| 구분 | 주요 명령 | 특징 |
|------|-------------|------|
| **DDL** | CREATE / ALTER / DROP | 구조 정의 (Auto Commit) |
| **DML** | SELECT / INSERT / UPDATE / DELETE | 데이터 조작 (트랜잭션 가능) |
| **DCL** | GRANT / REVOKE | 권한 제어 |

---

### 🔹 4. COMMIT & ROLLBACK

```sql
UPDATE EMP SET SAL = SAL + 100 WHERE DEPTNO = 10;
SAVEPOINT P1;
UPDATE EMP SET SAL = SAL - 50 WHERE DEPTNO = 20;
ROLLBACK TO P1;
COMMIT;
```

> ☑️ 부분 복구가 필요한 경우 `SAVEPOINT`를 적극 활용.

---

## ⚙️ 모델링 유의사항

- 트랜잭션 단위를 **업무 로직 단위**로 설계할 것  
- 다중 테이블 갱신 시, **데이터 무결성 제약**이 자동으로 오류를 탐지하도록 설계  
- DDL은 Auto Commit이므로 테스트 시 주의  
- ERD 설계 단계에서 **참조 무결성 (Foreign Key)** 관계를 명확히 명시  

---

## 🧮 실습 예제

### ✅ 1. 트랜잭션 제어
```sql
BEGIN TRANSACTION;
INSERT INTO EMP VALUES (101, 'KIM', 3000);
UPDATE DEPT SET TOTAL = TOTAL + 3000 WHERE DEPTNO = 10;
COMMIT;
```

### ✅ 2. 무결성 제약조건 테스트
```sql
ALTER TABLE EMP
ADD CONSTRAINT chk_sal CHECK (SAL > 0);
```

### ✅ 3. Auto Commit 확인
```sql
CREATE TABLE TEST (ID NUMBER);
-- Auto Commit 발생 (DDL 명령)
```

---

## 🧾 기출 포인트

| 구분 | 출제 유형 | 핵심 키워드 |
|------|------------|--------------|
| 개념형 | 트랜잭션 특성 | ACID, COMMIT, ROLLBACK |
| 응용형 | 무결성 제약조건 | PRIMARY, FOREIGN, CHECK |
| 실무형 | SQL 실행 순서 / Auto Commit | DDL vs DML, SAVEPOINT |

> 💡 DDL은 트랜잭션 대상이 아니며, DML만 ROLLBACK 가능.

---

## 💬 느낀점

트랜잭션과 무결성은 데이터베이스의 **신뢰성과 안전성의 근본**이었다.  
DDL과 DML의 차이를 명확히 구분하니, SQL 수행 시점의 흐름이 더욱 명료해졌다.  
특히 `SAVEPOINT`를 통한 부분 복구 개념은 실무형 문제에서 자주 활용될 수 있을 것 같다.

---

## 🔗 참고자료

- SQLD 공식 교재 Chapter 6 (트랜잭션과 무결성)
- DataEdu SQLD 강의 30~33강
- Oracle Docs – Transaction Control Statements
- https://docs.oracle.com/en/database/oracle/oracle-database/

---
