**Solutions for Hackerrank Advanced SQL Certifications**

## 1. Weather Analysis
```
SELECT MONTH(record_date) as m1,
       MAX(data_value) over(partition by MONTH(record_date)) as 'max_temp',
       MIN(data_value) over(partition by MONTH(record_date)) as 'min_temp',
       ( 
         SELECT AVG(data_value) over (partition by MONTH(record_date)) as `avg_temp`
         FROM temperature_records
         WHERE data_type = 'avg'
       ) as avg_1
FROM temperature_records
```

## 2. Winner's Chart
```
SELECT event_id,group_concat(first),
group_concat(second),
group_concat(third)
from 
(
SELECT event_id,
case when rnk =1 then group_concat(participant_name) end as first,
case when rnk =2 then group_concat(participant_name) end as second,
case when rnk =3 then group_concat(participant_name) end as third
from
(
SELECT event_id,participant_name,
dense_rank() OVER(partition by event_id order by m1 desc) as rnk
FROM 
(
   SELECT distinct(event_id),participant_name, 
   max(score) OVER(partition by participant_name,
   event_id) as m1
   from scoretable
)t0
)t1
GROUP BY event_id,rnk
)t2
group by event_id

```

## 3. Crypto Market Algorithms Report
```
select a1,group_concat(transactions_Q1),
group_concat(transactions_Q2),
group_concat(transactions_Q3),
group_concat(transactions_Q4)
from
(
select a1,
case when q1 = 1 then s1 end as transactions_Q1,
case when q1 = 2 then s1 end as transactions_Q2,
case when q1 = 3 then s1 end as transactions_Q3,
case when q1 = 4 then s1 end as transactions_Q4
from
(SELECT distinct(a1),q1,
round(sum(volume) over(partition by a1,q1),6) AS s1
FROM(
SELECT c1.algorithm as a1,quarter(t1.dt) as q1,
t1.volume
FROM coins c1
LEFT JOIN transactions t1 ON t1.coin_code= c1.code
where year(t1.dt) = '2020'
)v1
)v2
)v3
GROUP by a1
ORDER BY a1 ASC
```
