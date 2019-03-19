# MYSQL과 ORACLE의 차이

---

## NULL값 확인 함수가 다르다.

즉, 컬럼값에 NULL이면 다른값으로 표시해주는 함수사용법이 다릅니다.

ORACLE에서는 NVL함수를 사용하지만 MYSQL에서는 IFNULL을 사용합니다.

EX) SELECT NVL(USER_ID,'') FROM KGON

EX) SELECT IFNULL(USER_ID,'') FROM KGON

## 현재 날짜 시간 확인하는 방법이 다릅니다.

ORACLE에서는 SYSDATE를 사용하지만 MYSQL에서는 NOW() 함수를 사용합니다.

EX) SELECT SYSDATE FROM DUAL;

EX) SELECT NOW() FROM DUAL;

## 날짜포맷 변환 방법이 다릅니다.

ORACLE에서는 날짜를 STRING으로 변경시 TO_CHAR()함수를 사용하지만 MYSQL에서는 DATE_FORMAT()함수를 사용합니다.

EX) SELECT TO_CHAR(REG_DATE, 'YYYYMMDDHH24MISS' FROM DUAL;

EX) SELECT DATE_FORMAT(REG_DATE, '%Y%m%d%H%i%s') FROM DUAL;

[형식에 쓰는 영문자는 대소문자에 따라 다른값이 나올 수 있습니다.]

[%Y는 4자리년도(2017), %y는 2자리년도(17)]

## 네번째로 요일 변환의 숫자 범위가 다릅니다.

ORACLE은 일,월,화,수,목,금,토를 1,2,3,4,5,6,7로 인식합니다.

MYSQL은 일,월,화,수,목,금,토를 0,1,2,3,4,5,6으로 인식합니다.

[보통 자바스크립트에서 일,월,화,수,목,금,토를 0,1,2,3,4,5,6으로 쓰기 때문에 ORACLE의 경우 결과값을 -1해서 반환하는 경우가 많습니다.]

EX) SELECT TO_CHAR(SYSDATE, 'D') FROM DUAL; [결과값 : 오늘이 수요일인 경우 4를 반환]

EX) SELECT DATE_FORMAT(NOW(), '%w') FROM DUAL;

## 다섯번째로 문자와 문자 합치는 방법이 다릅니다.

ORACLE은 문자와 문자를 합칠 때 '||' 을 사용합니다.

MYSQL에서는 문자와 문자를 합칠 때 CONCAT() 함수를 이용합니다.

## 여섯번째로 **형변환**방법이 다릅니다.

ORACLE에서는 TO_CHAR, TO_NUMBER을 사용하여 형을 변환하지만 MYSQL에서는 CAST를 사용하여 형을 변환합니다.

ex) (ORACLE) SELECT TO_CHAR(632) FROM DUAL

ex) (MYSQL ) SELECT CAST(1234 AS CHAR) FROM DUAL

## 일곱번째로 **페이징처리**가 다릅니다.

ORACLE은 ROWNUM을 이용하여 WHERE에서 BETWEEN으로 1~10번째자료를 나타냅니다.

MYSQL은 LIMIT를 사용하여 1~10번째자료를 나타냅니다.

ex) (ORACLE) SELECT * FROM ( SELECT ROWNUM , A.* FROM (SELECT * FROM KGON) A )WHERE ROWNUM BETWEEN 0 AND 10

ex) (MYSQL ) SELECT * FROM KGON LIMIT 0, 10

## 여덟번째로 **시퀀스사용시 다음번호 불러오는 방법**이 다릅니다.

ORACLE은 시퀀스명.NEXTVAL을 사용하지만 MYSQL은 시퀀스명.CURRVAL를 사용합니다.