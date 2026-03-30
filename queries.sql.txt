select count(*)
from census;

SELECT income, count(*) as count
FROM census
group by income;

select income, avg(age) as avg_age
from census
group by income;

select "education-num", income, count(*) as count
from census
group by "education-num", income
order by "education-num";


SELECT "education_level", income, count(*) as count
from census
WHERE income = '>50K'
group by "education_level", income
order by count DESC;

SELECT "education_level" 
from census;

SELECT 
    education_level,
    SUM(CASE WHEN income = '>50K' THEN 1 ELSE 0 END) * 1.0 / COUNT(*) AS high_income_ratio
FROM census
GROUP BY education_level
ORDER BY high_income_ratio DESC;

select income, avg(age) as avg_age
from census
group by income;

select education_level
where income = '>50K' * 1.0 / count(*) as high_income_ratio
from census

SELECT "education_level", COUNT(*) AS total
FROM census
GROUP BY "education_level"
ORDER BY total DESC;

SELECT 
    "education_level",
    SUM(CASE WHEN income = '>50K' THEN 1 ELSE 0 END) * 1.0 / COUNT(*) AS high_income_ratio
FROM census
GROUP BY "education_level"
ORDER BY high_income_ratio DESC;

select education_level, count(*) as total
from census
group by education_level
order by total DESC;
------------------------
select 
	education_level, count(*) as total_people,
	sum(case when income = '>50K' then 1 else 0 end) as high_income_count,
	round( sum(case when income = '>50K' then 1 else 0 end) * 1.0 / count(*),
	3
	) as high_income_ratio
from census
group by education_level
order by total_people DESC;
--------------------------
select occupation, count(*) as high_income_count
from census
where income = '>50K'
group by occupation
order by high_income_count DESC;
--------------------------
select occupation, 
	count (*) as total_people,
	sum(case when income ='>50K' then 1 else 0 end) as high_income_count,
	round( sum(case when income ='>50K' then 1 else 0 end) * 1.0 / count(*), 3) as high_income_ratio
from census
group by occupation
order by high_income_count DESC;
--------------------------------
select education_level, occupation,
	count(*) as total_people,
	sum(case when income = '>50K' then 1 else 0 end) as high_income_count,
	round( sum(case when income = '>50K' then 1 else 0 end) * 1.0 / count(*),3) as high_income_ratio
	from census
	group by education_level, occupation
	order by total_people DESC, high_income_ratio ASC;
---------------------------------
SELECT *
FROM (
    SELECT 
        "education_level",
        occupation,
        COUNT(*) AS total_people,
        SUM(CASE WHEN income = '>50K' THEN 1 ELSE 0 END) AS high_income_count,
        ROUND(
            SUM(CASE WHEN income = '>50K' THEN 1 ELSE 0 END) * 1.0 / COUNT(*),
            3
        ) AS high_income_ratio
    FROM census
    GROUP BY "education_level", occupation
)
WHERE total_people < 10
ORDER BY high_income_ratio DESC;
--------------------------------------
SELECT *
FROM (
    SELECT 
        "education_level",
        occupation,
        COUNT(*) AS total_people,
        SUM(CASE WHEN income = '>50K' THEN 1 ELSE 0 END) AS high_income_count,
        ROUND(
            SUM(CASE WHEN income = '>50K' THEN 1 ELSE 0 END) * 1.0 / COUNT(*),
            3
        ) AS high_income_ratio
    FROM census
    GROUP BY "education_level", occupation
)
WHERE total_people > 100
ORDER BY high_income_ratio DESC;
-------------------------------------------
select *
from
(select occupation, education_level,
	count(*) as total_people,
	sum(case when income = '>50K' then 1 else 0 end) as high_income_count,
	round(sum(case when income = '>50K' then 1 else 0 end)*1.0 / count(*),3) as high_income_ratio
from census
group by education_level, occupation)
where total_people > 100
order by total_people DESC, high_income_ratio DESC ;
---------------------------------------------------	
select occupation, education_level,
	COUNT(*) AS total_people,
	sum(case when income = '>50K' then 1 else 0 end) as high_income_count,
	round(sum(case when income = '>50K' then 1 else 0 end) * 1.0/ count(*) ,3) as high_income_ratio
from census
group by education_level, occupation
having count(*) > 100
order by high_income_ratio DESC;
---------------------------------	
