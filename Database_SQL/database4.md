# Database & SQL Study

## 1. Sub-query

- 쿼리문 안에 쿼리가 있는 문법
- select, from, where

### 1-1. select 절의 서브쿼리

- ex) 전체 나라수, 전체 도시수, 전체 언어수를 출력

	```
	select 
	(select count(*)
	from country) as total_country,
	(select count(*)
	from city) as total_city,
	(select count(distinct(language))
	from countrylanguage) as total_language
	```

### 1-2. from 절의 서브쿼리

- ex) 800만 이상이 되는 도시의 국가 코드, 도시이름, 국가이름, 도시인구수를 출력

	```
	select * 
	from
		(select countrycode, name, population
		from city
		where population >= 8000000) as city_data
	join
		(select code, name
		from country) as country
	on city_data.countrycode = country.code
	```

### 1-3. where 절의 서브쿼리

- ex) 800만 이상 도시의 국가코드, 국가이름, 대통령이름 출력

	```
	select code, name, HeadOfState
	from country
	where code in (
		select distinct(countrycode)
		from city
		where population >= 8000000
		)
	```

## 2. Index
- 데이터를 검색할 때 빠르게 찾을 수 있도록 해주는 기능
- index는 저장공간을 차지하기 때문에 적절히 사용해야한다.
- index가 너무많으면 insert가 느려진다.
- 주로 where절에 사용되는 컬럼을 index로 사용해서 사용한다.

- employees database로 연습

	```
	use employees
	```

	```
	explain # 실행계획을 볼수있다.
	select count(*)
	from salaries
	where to_date > "2000-01-01"
	```

### 2-1. index 생성

	```
	create index tdate
	on salaries(to_date)
	```

### 2-2. index 삭제
	
	```
	drop index tdate
	on salaries
	```

## 3. View

- 특정 쿼리문에 대한 결과를 저장하는 개념

### 3-1. view 생성

	```
	create view code_name as
	select code, name
	from country
	```

- 생성 후 확인

	```
	select *
	from city
	join code_name # view
	on city.countrycode = code_name.code
	```