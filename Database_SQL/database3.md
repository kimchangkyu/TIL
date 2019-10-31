# Database & SQL Study

## 1. 소수점 올림, 반올림, 버림 함수

### 1-1. 올림(Ceil)

	```
	select ceil(12.345)
	```

### 1-2. 반올림(round)

	```
	select round(12.345, 2) # 둘째자리에서 반올림
	```

### 1-3. 버림(truncate)

	```
	select truncate(12.345, 2) # 둘째자리에서 버림
	```

## 2. 조건문

### 2-1. if


- if(조건, 참, 거짓)
- if는 select절에서 사용 가능

- ex) 도시의 인구가 100만 이상 big city, 100만 미만 small city를 출력, column : city_scale

	```
	select name, population,
	if (population >= 1000000, "big city", "small city") as city_scale
	from city
	```

### 2-2. ifnull


- ifnull(참, 거짓)
- 데이터에 null이면 거짓으로 치환, null이 아니면 참이 들어간다.

- ex) country 테이블에서 독립년도(IndepYear)가 없으면 0으로 출력

	```
	select Name, ifnull(IndepYear, 0) as IndepYear
	from country
	```

### 2-3. case

```
case 
	when (조건1) then (출력1)
	when (조건2) then (출력2)
end as (컬럼명)
```

- ex) 나라별 10억 이상, 1억 이상, 1억 이하 조건을 출력

```
select name, population,
case
	when population > 1000000000 then " upper 1 bilion"
	when population > 100000000 then " upper 100 milion"
	else "below 100 milion"
end as result
from country
```

## 3. DATE_FORMAT : 날짜 데이터의 포멧을 변경해주는 함수

- sakila database 에서 실습
use sakila

- ex) payment에서 월별 총 매출 출력

```
select date_format(payment_date, "%Y-%m") as monthly,
count(amount), sum(amount)
from payment
group by monthly
```

## 4. JOIN : pandas의 merge()함수와 같은 개념으로 생각한다.

- 연습을 위해서 world 데이터 베이스에 다음과 같이 테이블을 생성 후 insert

```
CREATE TABLE user (
	user_id int(11) unsigned NOT NULL AUTO_INCREMENT,
	name varchar(30) DEFAULT NULL,
	PRIMARY KEY (user_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE addr (
  	id int(11) unsigned NOT NULL AUTO_INCREMENT,
  	addr varchar(30) DEFAULT NULL,
	user_id int(11) DEFAULT NULL,
  	PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO user(name)
VALUES ("jin"),
("po"),
("alice"),
("petter");

INSERT INTO addr(addr, user_id)
VALUES ("seoul", 1),
("pusan", 2),
("deajeon", 3),
("deagu", 5),
("seoul", 6); 
```

### 4-1. inner join

	```
	select addr.addr, addr.user_id, user.name 
	from addr
	join user
	on addr.user_id = user.user_id # addr 테이블의 user_id, user 테이블의 user_id
	```

- world 도시이름, 국가이름을 출력

	```
	select city.countrycode, city.name, country.name
	from city
	join country
	on city.countrycode = country.code
	```

### 4-2. left join

	```
	select id, addr.addr, addr.user_id, ifnull(user.name, "-")
	from addr
	left join user
	on addr.user_id = user.user_id
	```

### 4-3. right join

	```
	select id, addr.addr, addr.user_id, user.name
	from addr # 먼저 쓴쪽이 left라고 생각하면된다.
	right join user
	on addr.user_id = user.user_id
	```

### 4-4. outer join

- mysql에서는 outer join이라는 것은 없다. => union으로 만들어낸다.

- union
	- elect 문의 결과를 합쳐서 출력
	- 자동으로 중복을 제거
	- 컬럼의 갯수가 맞아야 출력 가능

	```
	select name
	from user
	union all # all : 중복데이터까지 출력
	select addr
	from addr
	```

- union을 이용한 outer join
	- left join과 right join을 합친 결과라고 생각하면된다.

	```
	select user.name, addr.addr, addr.user_id
	from user
	left join addr
	on user.user_id = addr.user_id
	union
	select user.name, addr.addr, addr.user_id
	from user
	right join addr
	on user.user_id = addr.user_id
	```