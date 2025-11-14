# SQLD Day 25 – REGEXP 기반 패턴 매칭 및 문자열 분석 (2025-11-06)

## 🎯 학습 목표
- REGEXP 패턴 매칭의 기본 개념 이해
- 메타문자(., *, +, [], {}) 활용법 학습
- REGEXP_LIKE, REGEXP_REPLACE, REGEXP_SUBSTR 함수 활용

## 🧠 이론 정리

### 1️⃣ 정규표현식(Regular Expression) 기본 개념
정규표현식은 **문자열에서 특정 패턴을 찾거나 변환하기 위한 규칙 표현 방식**이다.

### 2️⃣ 주요 메타문자
| 메타문자 | 의미 | 예시 |
|---------|------|------|
| `.` | 임의의 한 문자 | a.c → abc, a1c |
| `*` | 0회 이상 반복 | ab*c → ac, abc, abbc |
| `+` | 1회 이상 반복 | ab+c → abc, abbc |
| `[]` | 문자 집합 | [0-9] 숫자 |
| `{n}` | n회 반복 | a{3} → aaa |

### 3️⃣ Oracle REGEXP 함수
| 함수 | 설명 |
|------|------|
| **REGEXP_LIKE(col, pattern)** | 패턴과 일치 여부 반환 |
| **REGEXP_SUBSTR(col, pattern)** | 패턴에 해당하는 부분 문자열 추출 |
| **REGEXP_REPLACE(col, pattern, replace)** | 패턴을 다른 문자열로 대체 |

---

## 🧪 예제
```sql
SELECT REGEXP_LIKE('A123', 'A[0-9]+') AS result FROM dual;
```

```sql
SELECT REGEXP_SUBSTR('010-1234-5678', '[0-9]{4}') FROM dual;
```

---

## 📝 요약
- 정규표현식은 문자열 패턴 분석의 핵심 도구.
- 숫자, 문자, 특정 규칙 기반 데이터 검증에 자주 사용.
- SQLD 2과목 실전 문제에서 자주 등장.

---

## 🔗 참고자료
- 아이리포 SQLD 강의 – 2과목 27강 REGEXP
