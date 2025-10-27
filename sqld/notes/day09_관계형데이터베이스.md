# **SQLD Day 09 – 관계형 데이터베이스 구조 및 제약조건 (2025-10-21)**
> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## **🎯 학습 목표**
- 관계형 데이터베이스(RDB)의 기본 구조 이해  
- 릴레이션(Relation), 튜플(Tuple), 속성(Attribute) 개념 명확화  
- 기본키, 외래키, 무결성 제약조건의 역할과 중요성 학습  

---

## **🧠 이론 정리**

### **1️⃣ 관계형 데이터베이스의 개념**
> 관계형 데이터베이스(Relational Database)는 데이터를 **행(Row)과 열(Column)** 구조로 관리하는 시스템이다.  
> 각 테이블은 **릴레이션(Relation)**, 한 행은 **튜플(Tuple)**, 한 열은 **속성(Attribute)** 에 해당한다.

| 구성 요소 | 설명 | 예시 |
|-----------|------|------|
| **릴레이션 (Relation)** | 데이터를 저장하는 테이블 구조 | EMP, DEPT |
| **튜플 (Tuple)** | 테이블의 한 행(Row) | 사원 한 명의 정보 |
| **속성 (Attribute)** | 테이블의 열(Column) | EMPNO, ENAME, SAL 등 |

> 💡 RDB는 **데이터의 독립성과 무결성**을 유지하면서도 **중복 최소화**를 목표로 한다.

---

### **2️⃣ 키(Key)의 종류**
> 릴레이션에서 튜플을 식별하거나 관계를 연결하기 위해 키를 사용한다.

| 키 종류 | 설명 | 예시 |
|----------|------|------|
| **기본키 (Primary Key)** | 튜플을 고유하게 식별하는 키 | EMPNO, DEPTNO |
| **후보키 (Candidate Key)** | 기본키가 될 수 있는 후보 | EMPNO, EMAIL |
| **대체키 (Alternate Key)** | 후보키 중 선택되지 않은 키 | EMAIL |
| **외래키 (Foreign Key)** | 다른 릴레이션의 기본키를 참조 | EMP.DEPTNO → DEPT.DEPTNO |
| **복합키 (Composite Key)** | 여러 속성으로 구성된 키 | (STUDENT_ID, SUBJECT_ID) |

> ⚙️ 키는 데이터의 **고유성(Unique)** 과 **참조무결성(Referential Integrity)** 을 보장한다.

---

### **3️⃣ 무결성 제약조건 (Integrity Constraints)**
| 구분 | 설명 | 예시 |
|------|------|------|
| **개체 무결성(Entity Integrity)** | 기본키는 NULL이 될 수 없음 | EMPNO NOT NULL |
| **참조 무결성(Referential Integrity)** | 외래키는 부모 테이블의 키를 참조해야 함 | DEPTNO REFERENCES DEPT(DEPTNO) |
| **도메인 무결성(Domain Integrity)** | 속성 값은 정의된 도메인 내에서만 허용 | GENDER IN ('M','F') |

> 💡 무결성은 데이터 신뢰성 확보의 핵심이며, **제약조건(CONSTRAINT)** 으로 구현된다.

---

## **⚙️ 모델링 유의사항**
1. 키 설계 시 중복을 최소화하고 명확한 식별 구조를 갖출 것  
2. 외래키 제약조건 설정 시 참조 테이블 삭제/수정 규칙(CASCADE, SET NULL 등) 고려  
3. 도메인 무결성은 ENUM, CHECK 제약 등으로 명시화  

---

## **⚙️ 핵심 요약**
- RDB는 행(Row)과 열(Column) 구조로 데이터를 저장한다.  
- 기본키는 개체 무결성을, 외래키는 참조 무결성을 보장한다.  
- 모든 속성은 도메인 제약을 가져야 하며, NULL 허용 여부를 명확히 정의해야 한다.  
- 제약조건을 올바르게 설정하면 데이터 품질이 향상된다.

---

## **🧮 예제 및 실습**
```sql
CREATE TABLE EMP (
  EMPNO NUMBER PRIMARY KEY,
  ENAME VARCHAR2(20) NOT NULL,
  DEPTNO NUMBER,
  CONSTRAINT fk_dept FOREIGN KEY (DEPTNO) REFERENCES DEPT(DEPTNO)
);
```
- [x] 기본키 및 외래키 제약조건 생성 실습  
- [x] CASCADE / SET NULL 동작 비교  
- [ ] CHECK 제약조건을 활용한 도메인 무결성 실습  

---

## **🧾 기출 복습**
| 회차 | 문항 | 주제 | 결과 | 비고 |
|------|------|------|------|------|
| 2023 2회 | Q41–Q45 | 무결성 제약조건 | ✅ | CASCADE와 SET NULL의 차이 확인 |
| 2022 1회 | Q36–Q40 | 기본키, 외래키, 도메인 제약 | ⚠ | CHECK 제약 구문 혼동 주의 |

> 📘 **기출 출처:**  
> SQLD 공식 교재 2권 ‘SQL 기본 및 응용’ **기출예상문제 2-3절 (p.130~138)** 기반 정리

---

## **💬 느낀점 / 메모**
- 관계형 모델은 단순한 테이블 구조가 아니라 **데이터 간 논리적 연결**을 설계하는 체계이다.  
- 제약조건을 통해 데이터의 일관성과 품질이 보장됨을 다시금 느꼈다.  
- 실무에서는 무결성 제약을 적절히 활용해 데이터 오류를 사전에 차단해야겠다.

---

## **🔗 참고자료**
- 아이리포 SQLD 강의 – 2과목 9강 (유튜브 9강): 관계형 데이터베이스 구조  
- SQLD 공식 교재 2권 p.29~48, p.130~138 (기출예상문제)  
- [관계형 데이터베이스 핵심 요약 – SQLGate 블로그](https://www.sqlgate.com/blog/relational-database-structure)
