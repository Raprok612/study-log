# SQLD Day 23 – 계층형 질의 CONNECT BY (2025-11-04)

## 🎯 학습 목표
- 계층형 질의(CONNECT BY PRIOR)의 구조 이해
- START WITH / CONNECT BY 동작 방식 정리
- PRIOR 키워드 방향성(순방향/역방향) 파악

## 🧠 이론 정리
### 1️⃣ 계층형 질의 개념
- 트리 구조(상위 → 하위)를 SQL 하나로 탐색하는 질의
- 부모–자식 관계를 명시적으로 표현해야 한다

```sql
SELECT LEVEL, empno, ename, mgr
FROM emp
START WITH mgr IS NULL
CONNECT BY PRIOR empno = mgr;
```

### 핵심 요소  
| 요소 | 의미 |
|-----|------|
| **START WITH** | 루트(시작 행) 지정 |
| **CONNECT BY** | 계층 관계 정의 |
| **PRIOR** | 부모/자식 방향 지정 |

---

### 2️⃣ PRIOR 방향
| 형태 | 의미 |
|------|------|
| PRIOR A = B | A가 부모, B가 자식 |
| A = PRIOR B | B가 부모, A가 자식 |

---

## 🧪 실습 메모
- 사원–관리자 구조를 트리로 출력  
- LEVEL 컬럼을 이용해 들여쓰기 구조 확인  
- 순방향/역방향 모두 테스트 완료

---

## ⚙️ 핵심 요약
- 계층형 질의는 트리 구조 표현 SQL  
- START WITH + CONNECT BY PRIOR 기반  
- PRIOR 위치에 따라 부모–자식 방향이 결정된다

---

## 📚 참고한 강의
- 아이리포 SQLD 강의 – **2과목 25강: 계층형 질의 예제**
