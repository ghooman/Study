## 📌MySQL 문법 정리

**<데이터조회하기 (SELECT)>**
```mysql
# 모든 컬럼을 선택할 때
SELECT * FROM 테이블명;

# 특정 컬럼을 선택할 때
SELECT column1, column2
FROM 테이블명;
```

**<검색 조건 지정하기 (WHERE)>**
```mysql
SELECT column1, column2 FROM 테이블명 WHERE 조건식;

# WHERE문 예제
SELECT * FROM 테이블명 WHERE price = 200; 
// price 값이 200인 경우만 조회

SELECT * FROM 테이블명 WHERE price <> 200; 
// price 값이 200이 아닌 경우만 조회

SELECT * FROM 테이블명 WHERE name = '홍길동';
// name이 홍길동인 경우만 조회
// 숫자가 아닌 문자열에 경우 ''를 붙인다.

SELECT * FROM 테이블명 WHERE name IS NULL;
// name이 NULL인 경우만 조회
```
