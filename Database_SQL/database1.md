# Database & SQL Study

## Structure 

- Server - Database - Table - Row

## 1. Create

### 1-1. Database
	- 데이터 베이스 확인
		- show databases; # 현재 데이터 베이스 확인

	- 생성
		- CREATE DATABASE test;

	- 선택
		- USE test;

	- 현재 확인
		- SELECT DATABASE();

### 1-2. Table
	- 생성
		- 테이블이름, 컬럼이름, 데이터타입 설정
			- create table user1(
				user_id int,
				name varchar(20),
				email varchar(30),
				age int(3),
				rdata date
				);

		- 제약사항
			- 종복 방지
			- null값 방지

			- primary key 설정
				- 중복되는 데이터가 들어갈 수 없다는 유니크 조건, null값 방지
			
			- auto_increment
				- 숫자를 1씩증가로 설정

			- unique
				- 중복을 피하는 조건
			
			- default
				- 데이터를 설정하지 않으면 자동으로 설정값으로 지정

			- timestamp
				- 데이터를 안넣어주면 현재시간으로 들어간다.

			- create table user2(
				user_id int primary key auto_increment,
				name varchar(20) not null,
				email varchar(30) unique not null,
				age int(3) default '30',
				rdata timestamp
				);

## 2. 수정(Alter)

### 2-1 데이터베이스 수정
	- `show variables like "character_set_database"`- 현재 데이터 베이스 인코딩 형식확인

	- 인코딩 변경
		- `alter database test character set = utf8`

### 2-2 테이블
	- `alter table user2 add tmp text` - 컬럼추가
	- `alter table user2 modify column tmp int(3)` - 타입 변경
	- `alter table user2 drop tmp` - 컬럼 삭제

## 3. 삭제(Drop)

### 3-1 데이터 베이스 삭제
	- `drop database tmp` - 데이터 베이스 삭제

### 3-2 테이블 삭제
	- `drop table user3` - 현재 데이터 베이스에 접속되어있는지를 확인하고 실행 

## 4. 데이터 삽입(Insert)
	- 테이블에 데이터를 삽입하는 것이다.

	```
	  insert into user1(user_id, name, email, age, rdate) 
	  value(2, "jin", "jin@gmail.com", 32, now()),
	  (3, "peter", "peter@gmail.com", 33, now()),
	  (4, "po", "po@gmail.com", 23, now()),
	  (5, "andy", "andy@gmail.com", 43, now()),
	  (6, "jin", "jin@gmail.com", 17, now())
	```

		- 원하는 컬럼만을 넣을수도있다.
		- now() : 현재시간(표준시간으로 들어간다.)

## 5. 데이터 조회(Select)
	- select ~ from ~
	
	```
	select user_id, name, age
	from user1
	```

	- 전체 조회
	```
	select *
	from user1
	```

### 5-1. Alias(as)
	- 출력할때 컬럼명을 변경할 수 있다.

	```
	select user_id as "ID", name as "UserName", age as "AGES"
	from user1
	```

### 5-2. 중복 제거(Distinct)
	```
	select distinct(name)
	from user1
	```

### 5-3. 조건 검색(Where)
	```
	select *
	from user1
	where age >= 40
	```
	
	- 30세 이상인 사용자를 검색해서 이름의 종류 갯수를 출력

		```
		select count(distinct(name))
		from user1
		where age >= 30
		```
		- count : 데이터의 갯수를 출력

	- 논리 연산자도 사용가능
		
		```
		select *
		from user1
		where age >= 20 and age < 40
		```

### 5-4. between A and b(범위별로 가져올 때)
	```
	select *
	from user1
	where age between 23 and 40
	```

### 5-5. 정렬(Order by)
	- 오름차순(ascending) - default, 생략가능

	```
	select *
	from user1
	order by age asc
	```

	- 내림차순(descending)
	- name으로 오름차순을 하고, 같은 이름을 가진것들은 나이로 정렬을 한다는 의미
	
    ```
    select *
    from user1
    order by name, age desc
    ```

### 5-6. concat(데이터 합치기)
	```
	select name, age, concat(name,"(", age, ")") as "name_age"
	from user1
	```

### 5-7. like
	- where절에서 특정 문자열이 들어간 데이터 조회할때 사용
	- "%" : 문자가 있거나 없거나

	```
	select * 
	from user1
	where email like "%@gamil.%"
	```
	
	- not like : 특정 문자가 들어가지 않은것을 찾을때

	```
	select * 
	from user1
	where email not like "%@gamil.%"
	```

### 5-8. in
	- 여러개의 조건을 조회할때 사용

	```
	select * 
	from user1
	where name in ("andy", "peter", "po")
	```

	- 서브쿼리를 이용
	
	```
	select * 
	from user1
	where name in (
		select distinct(name)
		from user1
		where age > 30
	)
	```

### 5-9. Limit
	- 제한을 해준다.
	
	- 가장 상단에 있는 3개를 출력

	```
	select * 
	from user1
	limit 3
	```
	
	- 3번째 부터 밑으로 5개를 출력

	```
	select *
	from user1
	limit 3, 5
	```

## 6. Update
	- 조건을 주고 업데이트

	```
	update user1
	set age=20, rdate="2019-12-12"
	where age between 20 and 29
	```

## 7. 삭제(Delete)
	```
	delete from user1
	where rdate > "2019-11-01"
	```