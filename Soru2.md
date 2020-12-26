# 1980’den itibaren herhangi bir spor grubunda üst üste 3 veya daha fazla madalya almış atletleri bulalım.


``` SQL
with threeYearTable as(

  with champions as (
  select athlete, year
  from berker_ot.summer_medals
  where year > 1980 and medal = 'Gold' or medal = 'Silver' or medal = 'Bronze'
  group by year, athlete
  
)
select 
athlete, 
last_value(year) over (partition by athlete order by year rows between 1 preceding and 1 following) as next_year,
year as currentYear,
first_value(year) over (partition by athlete order by year rows between 1 preceding and 1 following) as past_year
from champions
)
select distinct athlete
from ThreeYearTable
where next_year = currentYear + 4 and past_year = currentYear - 4
order by athlete

```
