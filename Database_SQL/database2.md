# Database & SQL Study

## 1. group by
	- 중복되는 값들을 묶어준다.
	- count로 갯수를 세준다.

	- city 테이블에서 나라별 도시의 갯수를 출력

	```
	select CountryCode, count(CountryCode) as count
	from city
	group by CountryCode
	```
	
	- countrylanguage테이블에서 전체 언어의 갯수를 출력

	```
	select count(distinct(Language)) 
	from countrylanguage
	```

	- 대륙별 인구수와 GNP의 최대값을 출력
	- max() : 최대값
	- sum() : 합

	```
	select Continent, max(Population), max(GNP), sum(GNP) / sum(Population)
	from country
	group by Continent
	```

## 1-1. Having
	- Having : group by가 실행되고 난 결과에 조건을 추가

	- 대륙별 전체인구를 구하고 5억 이상인 대륙만 출력

	```
	select Continent, sum(Population) as data
	from country
	group by Continent
	having data > 500000000
	```

## 데이터 타입
	- 데이터 베이스의 테이블을 생성할때 각 컬럼은 데이터 타입을 가집니다.

## 1. Numberic

### 1-1. 정수 타입 (integer types)

### 1.2 고정 소수점 타입 (ﬁxed-point types)
	- DECIMAL(M, D)
	- M : 소수점을 포함한 전체 자리수
	- D : 소수 부분 자리수

### 1.3 실수 (ﬂoating-point types)
	- 소수점을 나타내기 위한 데이터 타입으로 아래의 두가지 데이터 타입이 있습니다. 
    - 두가지의 데이터 타입 은 데이터 저장공간의 차이가 있습니다.
	- FLOAT (4byte), DOUBLE (8byte)

### 1.4 비트 값 타입 (bit value type)
	- 0과 1로 구성이 되는 2진수(binary) 데이터를 나타냅니다.

	BIT(M)
	- M은 비트의 범위를 나타냅니다. 예를들어  M을 5로 작성하면 00000(2) ~ 11111(2) 까지 표현이 가능 합니다

## 2 Date & Time

### 2.1 DATE
	- DATE는 날짜를 저장하는 데이터 타입이며, 기본 포멧은 "년-월-일" 입니다.

### 2.2 DATETIME
	- DATETIME은 날짜와 시간을 저장하는 데이터 타입이며, 기본 포멧은 "년-월-일 시:분:초" 입니다.

### 2.3 TIMESTAME
	- TIMESTAME는 날짜와 시간을 저장하는 데이터 타입 
	- DATETIME과 다른점은 날짜를 입력하지 않 으면 현재 날짜와 시간을 자동으로 저장할수 있는 특징이 있습니다.

### 2.4 TIME
	- TIME은 시간을 저장하는 데이터 타입이며, 기본 포멧은 "시:분:초" 입니다.

### 2.5 YEAR
	- YEAR는 연도를 저장할수 있는 데이터 타입입니다.
	- YEAR(2)는 2자리의 연도를 저장할수 있으며 YEAR(4)는 4자리의 연도를 저장할수 있습니다.

## 3. String

### 3-1. CHAR(4)
	- ' ' : 4 bytes
	- 'ab' : 4 bytes
	- 'abcd' : 4 bytes

### 3-2. VARCHAR(4)
	- ' ' : 1 bytes
	- 'ab' : 3 bytes
	- 'abcd' : 5 bytes