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

SELECT animal_type, count(animal_type) as count // anmial_type을 가져오고, 그 개수를 띄워주는데 count라고 명칭
from animal_ins //테이블 이름
group by animal_type // animal_type별로 특정 컬럼을 그룹화하는 group by
order by animal_type // animal_type순으로 정렬



-- 코드를 입력하세요
SELECT name, count(name) as count   //출력문
from animal_ins // 테이블
group by name // name그룹으로 데이터를 그룹화
having count > 1 // 그룹에 조건을 걸땐 having이여야한다.
order by name // 정렬

-- 코드를 입력하세요
SELECT hour(datetime) as hour, count(datetime) as count //hour은 시간이다.
from animal_outs
where hour(datetime) >= 9   //항상 select from where이다. 속성을 기준으로 하는거기 때문에 where을 쓴다.
    and hour(datetime) <= 19

group by hour
order by hour
```



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
