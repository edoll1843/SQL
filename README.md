# SQL
```sql

//sqld의 기본 구조
select 속성
from 테이블       
where 조건           

// 정렬 
order by 속성 desc // 내림차순
order by 속성      // 오름차순

//출력의 명칭 바꾸는 as
SELECTE MAX/MIN/SUM/COUNT(속성이름) AS '출력의 명칭'

// 중복 제거
SELECT COUNT(DISTINCT NAME) AS 'count'    <--- DISTINCT 속성 중복 제거 속성 앞에 붙어야한다.
FROM 테이블

// 갯수 제한
SELECT name 
from animal_ins
order by datetime
limit 1            // limit로 갯수를 제한 걸 수 있다.

// null이 아닌
where 속성 is not null

// 종류별로 묶는다.
group by 속성

// 종류별로 묶고 조건문
group by 속성
having 조건 // 이때 having은 group by 바로 뒤에 나와야한다.

// 날짜 데이터에서 일부만 추출하기
YEAR(기준 날짜)
MONTH(기준 날짜)
DAY(기준 날짜)
HOUR(기준 날짜)
MINUTE(기준 날짜)
SECOND(기준 날짜)

// where 절의 조합(AND/OR/NOT/IN)
and == &&
or == ||
not == !=

// 변수 선언
SET @변수명 := 초기값;   // 세미콜론 꼭 있어야함

// null 처리
속성의 데이터가 null이면 다른 방법으로 바꿀 수가 있다.
ifnull(검사할 속성, '대체할 값')







```sql
2021/08/24
모든 레코드 조회하기
ANIMAL_INS테이블에서 모든 정보를
ANIMAL_ID의 오름차순으로 출력한다.
-- 코드를 입력하세요
SELECT *   //전부
from ANIMAL_INS // 테이블
order by ANIMAL_ID // order by로 오름차순 ANIMAL_ID기준
```
```sql
NAME, DATETIME을 출력하는데 내림차순으로 정렬한다.
-- 코드를 입력하세요
SELECT NAME, DATETIME
from ANIMAL_INS
order by ANIMAL_ID desc // order by desc <-- 내림차순 , asc <-- 오름차순
```
```sql
animal_id, name을 출력하는데
동물의 컨디션이 sick이 조건으로 들어간다.
-- 코드를 입력하세요
SELECT animal_id, NAME
from ANIMAL_INS
where intake_condition = 'Sick'
```
```sql
animal_id, name을 출력하는데
동물의 컨디션이 aged가 아닌 것을 고른다.
-- 코드를 입력하세요
SELECT animal_id, name
from animal_ins
where intake_condition != "aged"
order by animal_id
```
```sql
동물의 id순으로 오름차순 정렬 
-- 코드를 입력하세요
SELECT animal_id, name
from animal_ins
order by animal_id asc
```
```sql
동물의 이름순으로 정렬하는데 같은 이름이 있으면 역순으로 정렬한다.
distinct를 써야하나 생각했는데 결과값은 같음.
-- 코드를 입력하세요
SELECT animal_id, name, datetime
from animal_ins
order by name, datetime desc
```
```sql
동물의 이름을 출력하는데 제일 먼저 들어온 동물을 출력한다.
-- 코드를 입력하세요
SELECT name 
from animal_ins
order by datetime
limit 1
```
```sql
가장 늦게 들어온 동물을 '시간'으로 출력한다.
min, count이 다음문제들 
SELECT MAX(DATETIME) AS '시간'
FROM ANIMAL_INS
```
```sql
동물의 이름은 몇개인지 출력하고 null인경우는 집계하지 않고
중복되는 이름은 하나로 친다.
-- 코드를 입력하세요
SELECT count(distinct name) as 'count'
from animal_ins
where name is not null
```
```sql
동물의 타입은 cat, dog밖에없는데 이 동물들 타입별로 각각 몇마리인지
조회한다. 이때 고양이를 개보다 먼저 조회한다. <-- 타입을 정렬
select animal_type, count(animal_type) as 'count'
from animal_ins
group by animal_type //같은 종류별로 그룹화한다.
order by animal_type
```
```sql
동물의 이름 중 두번 이상 쓰인 동물의 이름과, 횟수를 출력한다.
select name, count(name) as 'count'
from animal_ins
group by name
having count > 1  //where은 그룹화하기 전에 쓰임, having은 group by 후에 쓰는데
// having count는 select에서 'count'로 바꾼 속성을 말한다.
order by
```
```sql
09시부터 19:59분까지 각 시간대 별로 입양이 몇 건이 발생했는지 알아보려고 한다.
select hour(datetime) as 'hour', count(animal_id) as 'count'
from animal_outs
where hour(datetime) >=9 and hour(datetime) <=19 
group by hour
order by hour
```
```sql
몇시에 가장 활발하게 일어나는지 각 시간대 별로 입양이 몇 건이나 발생했는지 찾는다.
이때 결과는 시간대 순으로 정렬
set @hour := -1;     //변수 선언
select (@hour := @hour +1) as hour , (
    select count(*)
    from animal_outs
    where hour(datetime) = @hour ) as 'count'
from animal_outs
where @hour < 23
group by animal_id
order by hour
```
```sql
이름이 없는 동물의 아이디를 출력한다.
-- 코드를 입력하세요
SELECT animal_id
from animal_ins
where name is null
```
```sql
이름이 있는 동물을 출력한다.
-- 코드를 입력하세요
SELECT animal_id
from animal_ins
where name is not null
order by animal_id
```
```sql
이름이 null인 것은 no name으로 처리해준다.
SELECT animal_type,  ifnull(name,"No name") as 'name', sex_upon_intake
from animal_ins
order by animal_id
```
