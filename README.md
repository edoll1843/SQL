# SQL
```sql
SELECTE MAX/MIN/SUM/COUNT(속성이름) AS '출력의 명칭'

FROM  테이블


SELECT COUNT(DISTINCT NAME) AS 'count'    <--- DISTINCT 속성 중복 제거 속성 앞에 붙어야한다.
FROM 테이블


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
