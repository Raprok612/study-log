# **SQLD Day 12 – 문자함수 (TRIM, SUBSTR 등) 및 함수 동작 원리 (2025-10-24)**

> 📘 SQLD 2과목 | SQL 기본 및 응용  
> 🧑‍💻 학습자: Jaerok Kim (Raprok612)

---

## 🎯 학습 목표
- 문자열 처리 함수의 구조 이해  
- TRIM / SUBSTR / LENGTH 등의 주요 문자함수 동작 방식 숙지  
- Oracle/ANSI SQL 함수 차이 파악  

---

## 🧠 이론 정리

### 1️⃣ TRIM 함수

| 함수 | 설명 | 예시 |
|------|------|------|
| **TRIM** | 앞/뒤 공백 제거 | `TRIM('  ABC  ') → 'ABC'` |
| **LTRIM** | 왼쪽 공백 제거 | `LTRIM('  ABC')` |
| **RTRIM** | 오른쪽 공백 제거 | `RTRIM('ABC  ')` |

---

### 2️⃣ SUBSTR / LENGTH

| 함수 | 설명 | 예시 |
|------|------|------|
| **SUBSTR(str, pos, len)** | 특정 위치부터 부분 문자열 | `SUBSTR('ORACLE', 2, 3) → 'RAC'` |
| **LENGTH(str)** | 문자열 길이 | `LENGTH('ABC') → 3` |

> Oracle은 문자열 index가 **1부터 시작**한다.

---

### 3️⃣ INSTR

문자열 내 특정 문자 위치를 찾는 함수  
예:  
```sql
INSTR('ORACLE SQL', 'SQL')  → 8
```

---

### 4️⃣ CONCAT / || 연산자
문자열 결합  
```sql
SELECT 'Hello ' || 'World' FROM dual;
```

---

## 🧮 실습

```sql
SELECT 
  TRIM('  SQLD  '),
  SUBSTR('DATABASE', 5, 3),
  INSTR('ABCABC', 'B')
FROM dual;
```

---

## 💬 느낀점
- 문자열 처리 함수는 SQLD 실전에서 매우 자주 출제됨  
- 특히 TRIM 동작 방식과 SUBSTR index 개념은 반복 학습 필요  

---

## 🔗 참고자료
- 아이리포 SQLD 강의 – 12강  
- SQLD 공식 교재 2권 p.140~156
