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
