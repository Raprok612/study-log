# **SQLD Day 20 – 트랜잭션, 무결성, DDL·DML 종합 복습 (2025-11-01)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**

- 트랜잭션(Transaction)의 개념과 ACID 특성 완전 이해  
- 무결성 제약조건의 종류 및 작동 방식 숙지  
- DDL, DML, DCL의 차이점과 Auto Commit 메커니즘 파악  
- COMMIT, ROLLBACK 실습을 통한 트랜잭션 제어 흐름 이해

---

## **🧠 이론 정리**

### **1️⃣ 트랜잭션 (Transaction)**

> 데이터베이스의 논리적 작업 단위로, 모든 연산이 완전하게 수행되어야 한다.

| 속성 | 의미 | 설명 |
|------|------|------|
| **A (Atomicity)** | 원자성 | 전부 수행되거나 전혀 수행되지 않음 |
| **C (Consistency)** | 일관성 | 트랜잭션 전후 데이터 무결성 유지 |
| **I (Isolation)** | 고립성 | 동시에 수행되는 트랜잭션 간 간섭 방지 |
| **D (Durability)** | 지속성 | COMMIT된 데이터는 영구 반영 |

```sql
BEGIN TRANSACTION;
UPDATE ACCOUNT SET BALANCE = BALANCE - 1000 WHERE ID = 'A';
UPDATE ACCOUNT SET BALANCE = BALANCE + 1000 WHERE ID = 'B';
COMMIT;
```

> ⚠️ 하나라도 실패 시 ROLLBACK으로 복원해야 함.

---

### **2️⃣ 무결성 제약조건 (Integrity Constraints)**

| 제약조건 | 설명 | 예시 |
|-----------|--------|------|
| **PRIMARY KEY** | 고유 식별자 (NULL 불가, 중복 불가) | `PRIMARY KEY (EMP_ID)` |
| **FOREIGN KEY** | 다른 테이블의 기본키 참조 | `FOREIGN KEY (DEPT_ID) REFERENCES DEPT(DEPT_ID)` |
| **UNIQUE** | 중복 불허 | `UNIQUE (EMAIL)` |
| **NOT NULL** | NULL 불허 | `NOT NULL` |
| **CHECK** | 조건식 검증 | `CHECK (AGE >= 18)` |

> 💡 FK 제약조건 옵션: `ON DELETE CASCADE`, `ON DELETE SET NULL`

```sql
ALTER TABLE EMP
ADD CONSTRAINT fk_dept FOREIGN KEY (DEPTNO)
REFERENCES DEPT(DEPTNO) ON DELETE CASCADE;
```

---

### **3️⃣ DDL / DML / DCL 비교**

| 구분 | 주요 명령 | 특징 | 트랜잭션 가능 여부 |
|------|------------|--------|----------------|
| **DDL** | CREATE / ALTER / DROP | 구조 정의 명령 | ❌ Auto Commit 발생 |
| **DML** | SELECT / INSERT / UPDATE / DELETE | 데이터 조작 명령 | ✅ ROLLBACK 가능 |
| **DCL** | GRANT / REVOKE | 권한 제어 | ✅ 트랜잭션 가능 |

```sql
CREATE TABLE TEST (ID NUMBER);
-- DDL 명령 → Auto Commit 발생

INSERT INTO TEST VALUES (1);
ROLLBACK;  -- DML → ROLLBACK 가능
```

---

### **4️⃣ COMMIT, ROLLBACK, SAVEPOINT**

```sql
UPDATE EMP SET SAL = SAL + 100 WHERE DEPTNO = 10;
SAVEPOINT P1;
UPDATE EMP SET SAL = SAL - 50 WHERE DEPTNO = 20;
ROLLBACK TO P1;
COMMIT;
```

| 명령 | 의미 | 비고 |
|------|------|------|
| **COMMIT** | 변경 내용을 DB에 반영 | 영구 저장 |
| **ROLLBACK** | 변경 내용 취소 | 마지막 COMMIT 시점으로 복원 |
| **SAVEPOINT** | 중간 복구 지점 설정 | 부분 복원 가능 |

---

## **⚙️ 모델링 유의사항**

1. 트랜잭션 단위는 **업무 로직 단위**로 설계  
2. FK 제약조건은 **참조 무결성 자동 보장 장치**  
3. DDL 명령은 Auto Commit이므로 테스트 시 주의  
4. ERD 설계 시, **PK–FK 관계 및 무결성 옵션** 반드시 명시  

---

## **🧮 예제 및 실습**

**예제 1️⃣ – 트랜잭션 제어 실습**
```sql
BEGIN TRANSACTION;
INSERT INTO EMP VALUES (101, 'KIM', 3000);
UPDATE DEPT SET TOTAL = TOTAL + 3000 WHERE DEPTNO = 10;
COMMIT;
```

**예제 2️⃣ – 무결성 제약조건 테스트**
```sql
ALTER TABLE EMP
ADD CONSTRAINT chk_sal CHECK (SAL > 0);
```

**예제 3️⃣ – DDL Auto Commit 확인**
```sql
CREATE TABLE TEMP (ID NUMBER);
-- DDL 실행 즉시 COMMIT 발생
```

- [x] COMMIT / ROLLBACK 실습 완료  
- [x] 제약조건 옵션(CASCADE / SET NULL) 검증  
- [x] DDL Auto Commit 테스트 완료

---

## **🧾 기출 복습**

| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2024 2회 | Q81–Q85 | 트랜잭션과 COMMIT / ROLLBACK | ✅ | SAVEPOINT 구문 숙지 |
| 2023 1회 | Q76–Q80 | 무결성 제약조건 | ✅ | FK 옵션 구분 |
| 2022 2회 | Q71–Q75 | DDL / DML 차이 | ⚠ | Auto Commit 혼동 주의 |

> 📘 기출 출처: SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ 2-17절~2-18절 (p.244~260)

---

## **💬 느낀점 / 메모**

- 트랜잭션의 원자성(Atomicity)과 무결성(Consistency)의 관계를 명확히 이해했다.  
- 실무에서는 단순 COMMIT보다 SAVEPOINT를 활용한 부분 복구가 중요함을 느꼈다.  
- DDL 명령이 Auto Commit이라는 점을 실습으로 확인하여, 개발 시 주의가 필요함을 체감했다.

---

## **🔗 참고자료**

- 아이리포 SQLD 강의 – 2과목 30~33강 (유튜브 30~33강): 트랜잭션 / 무결성 / DDL·DML 종합 복습  
- SQLD 공식 교재 2권 p.244~260  
- [Oracle Transaction Control Statements](https://docs.oracle.com/en/database/oracle/oracle-database/)  
- [아이리포 공식 유튜브 채널 – SQLD 모든 것](https://www.youtube.com/@irepo_official)
