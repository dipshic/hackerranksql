# Hackerrank SQL
** Solutions for Hackerrank SQL questions - Medium Level. **

## 1. Advanced Select - Occupations
```
set @r1=0, @r2=0, @r3=0, @r4=0;
select min(doctor), min(professor), min(singer), min(actor)
from(
select case
    when occupation = 'Doctor' then @r1:= @r1+1
    when occupation = 'professor' then @r2:= @r2+1
    when occupation = 'singer' then @r3:= @r3+1
    when occupation = 'actor' then @r4:= @r4+1 
    end as row_index,
    
    case when occupation ='Doctor' then name end as doctor,
    case when occupation ='professor' then name end as professor,
    case when occupation ='Singer' then name end as Singer,
    case when occupation ='Actor' then name end as Actor 
from occupations
    order by name) as temp
group by row_index;
```


## 2. Advanced Select - The Pads
```
SELECT CONCAT(Name,'(',LEFT(Occupation,1),')')
FROM OCCUPATIONS
ORDER BY Name ASC;
SELECT CONCAT('There are a total of ',COUNT(*),' ', LOWER(Occupation),'s.')
FROM OCCUPATIONS
GROUP BY Occupation
ORDER BY COUNT(*),Occupation ASC;
```

## 3. Advanced Select - New Companies
```
select c.company_code, c.founder, 
    count(distinct lm.lead_manager_code) as tot_lm , 
    count(distinct sm.senior_manager_code) as tot_sm,
    count(distinct m.manager_code) as tot_managers, 
    count(distinct e.employee_code) as tot_emp
from (select distinct * from company) c
inner join (select distinct * from lead_manager) lm
on c.company_code = lm.company_code
inner join (select distinct * from senior_manager) sm
on lm.company_code = sm.company_code
inner join (select distinct * from manager) m
on sm.company_code = m.company_code 
inner join (select distinct * from employee) e
on m.company_code = e.company_code
group by c.company_code, c.founder
order by company_code;
```

## 4. Advanced Select - Weather Observation Station 18
```
SELECT 
    ROUND(ABS(MIN(LAT_N)-MAX(LAT_N))+ ABS(MIN(LONG_W)-MAX(LONG_W)),4)
FROM STATION;
```

## 5. Advanced Select - Weather Observation Station 19
```
SELECT 
    ROUND(SQRT(POW(MIN(LAT_N)-MAX(LAT_N),2)+POW(MIN(LONG_W)-MAX(LONG_W),2)),4)
FROM STATION;
```

## 6. Advanced Select - Weather Observation Station 20
```
SET @r = 0;
SELECT ROUND(AVG(Lat_N), 4)
FROM (SELECT (@r := @r + 1) AS r, Lat_N FROM Station ORDER BY Lat_N) Temp
WHERE
    r = (SELECT CEIL(COUNT(*) / 2) FROM Station) OR
    r = (SELECT FLOOR((COUNT(*) / 2) + 1) FROM Station);
```

## 7. Advanced Select - The Report
```
select if (grade < 8, null, s.name), g.grade, s.marks
from students s, grades g
where marks between min_mark and max_mark
order by g.grade desc, name;
```
