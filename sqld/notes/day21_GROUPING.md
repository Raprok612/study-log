# **SQLD Day 21 – ROLLUP · CUBE · GROUPING 완전 정복 (2025-11-02)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- ROLLUP, CUBE, GROUPING 함수의 구조 완전 이해  
- 집계 단계별 생성 규칙 파악  
- GROUPING() → 1(집계행) / 0(일반행) 완벽 구분  

---

## 🧠 이론 정리

### 1️⃣ ROLLUP  
> **계층적(Top-down)** 으로 합계 생성  

예) `GROUP BY ROLLUP(deptno, job)`

생성 순서  
1) (deptno, job)  
2) (deptno)  
3) 전체 총계(NULL)

---

### 2️⃣ CUBE  
> **모든 조합** 에 대해 집계 생성  

예) `GROUP BY CUBE(deptno, job)`

생성  
- (deptno, job)  
- (deptno)  
- (job)  
- ()

---

### 3️⃣ GROUPING() 함수  
> 집계행 여부 확인 함수  
- **1 = 집계행(Aggregate row)**  
- **0 = 일반행(Detail row)**

```sql
SELECT deptno, job,
       SUM(sal),
       GROUPING(deptno) AS g1,
       GROUPING(job) AS g2
FROM emp
GROUP BY ROLLUP(deptno, job);
```

---

## 🧮 실습 체크리스트
- [x] ROLLUP / CUBE 구조 비교  
- [x] GROUPING = 1 / 0 케이스 구분  
- [x] ROLLUP → 부모-자식 계층 확인  

---

## ⚙️ 핵심 요약
- ROLLUP: 단계별 합계 / CUBE: 모든 조합  
- GROUPING 함수 없이는 집계행 구분 불가  
- SQLD 실전에서 가장 자주 출제되는 고난도 파트  

---

## 🔗 참고자료
- 아이리포 SQLD 21강  
- SQLD 공식 교재  
