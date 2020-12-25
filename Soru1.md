# Soru 1) 1980’den itibaren spor grubu bazında en çok madalya alan 1. 3. 5. ülkeyi bulalım.

``` SQL 
with ranksTable as (select
country,
sport,
rank() over(partition by sport order by medals desc) as rank
from (select country, sport, Count(medal) as medals
    from berker_ot.summer_medals
    where year > 1980 and medal is not null
    group by sport,country order by sport,medals desc))
select sport, country , rank
from ranksTable
where rank in (1,3,5)
order by sport, rank;

```
