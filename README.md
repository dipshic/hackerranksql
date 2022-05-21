# Hackerrank SQL
Solutions for Hackerrank SQL questions.

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


