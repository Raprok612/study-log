# **SQLD Day 27 – COMMIT·ROLLBACK·제약조건·DELETE 계열 총정리 (2025-11-08)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**

- 트랜잭션(Transaction) 개념과 동작 구조 이해  
- COMMIT / ROLLBACK 실행 흐름 복습  
- 참조무결성 제약조건(CASCADE / SET NULL) 정리  
- DROP / TRUNCATE / DELETE 차이 완벽 정리  

---

## **🧠 이론 정리**

### **1️⃣ 트랜잭션(Transaction)의 개념**

> 데이터베이스의 논리적 작업 단위로,  
> ACID 특성을 만족해야 한다.

- **A (Atomicity)** 원자성  
- **C (Consistency)** 일관성  
- **I (Isolation)** 고립성  
- **D (Durability)** 지속성  

---

### **2️⃣ COMMIT & ROLLBACK**

| 명령어 | 설명 |
|-------|------|
| **COMMIT** | 모든 변경 내역을 영구 저장 |
| **ROLLBACK** | 변경 사항 취소, 이전 상태 복구 |
| **SAVEPOINT** | ROLLBACK 지점 설정 |

---

### **3️⃣ 참조 무결성 제약조건**

| 옵션 | 설명 | 예시 |
|------|------|------|
| **ON DELETE CASCADE** | 부모 삭제 시 자식도 자동 삭제 | 회원 삭제 → 주문 삭제 |
| **ON DELETE SET NULL** | 부모 삭제 시 자식 FK 값을 NULL로 변경 | 회원 삭제 → 주문의 회원ID NULL |

---

### **4️⃣ DROP / TRUNCATE / DELETE 비교**

| 명령어 | 설명 | 트랜잭션 | 복구 가능 여부 |
|--------|------|----------|----------------|
| **DELETE** | 조건에 맞는 행 삭제 | O | O |
| **TRUNCATE** | 테이블 모든 데이터 삭제 | X | X |
| **DROP** | 테이블 구조 자체 삭제 | X | X |

---

## **⚙️ 핵심 요약**

- 트랜잭션은 SQL 작업의 안정성을 보장하는 핵심 개념이다.  
- COMMIT은 저장, ROLLBACK은 취소이며 SAVEPOINT로 구간 제어가 가능하다.  
- CASCADE·SET NULL은 참조무결성 처리 방식에서 매우 자주 출제된다.  
- DROP/TRUNCATE/DELETE는 시험 단골 비교 문제이다.

---

## **🧮 예제**

```sql
DELETE FROM EMP WHERE DEPTNO = 10;
ROLLBACK;

ALTER TABLE EMP
ADD CONSTRAINT fk_dept
FOREIGN KEY (DEPTNO)
REFERENCES DEPT(DEPTNO)
ON DELETE SET NULL;
```

---

## **💬 느낀점**

- SQL 작업의 안정성을 위해 트랜잭션 개념은 필수라는 것을 다시 확인했다.  
- DROP/TRUNCATE/DELETE는 실전에서 실수하면 복구 불가이므로 확실히 익혀야 한다.  
- 제약조건의 옵션(CASCADE/SET NULL)은 실제 업무에서도 자주 쓰이므로 중요하다.

---

## **📚 참고한 강의**

- 아이리포 SQLD 강의 – 30강: 트랜잭션 & TCL  
- 아이리포 SQLD 강의 – 31강: COMMIT / ROLLBACK 문제 해설  
- 아이리포 SQLD 강의 – 32강: 참조 무결성 제약조건  
- 아이리포 SQLD 강의 – 33강: DROP / TRUNCATE / DELETE 차이
