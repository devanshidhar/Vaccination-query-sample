# Vccination query


## All entries as on date i.e 28-08-2021

``` sql
SELECT  * FROM `bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights` WHERE DATE(_PARTITIONTIME) = "2021-08-28" LIMIT 1000 
```

![1](https://user-images.githubusercontent.com/88762643/131224384-3042a806-c54e-48a0-b46c-0b069d60e7ac.PNG)


## Counting the total no. number of sub regions  
SELECT count(sub_region_1) FROM `bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights`

![2](https://user-images.githubusercontent.com/88762643/131224322-83091467-92e0-476c-b9f9-6a54d04976a6.PNG)

## start date and last date of vaccoination in 2021

SELECT min(date) as start_date, max(date) as last_date FROM `bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights` LIMIT1000

![3](https://user-images.githubusercontent.com/88762643/131229211-0f0d8107-82f3-47be-86db-ba7afe2af95a.PNG)

## No. of vaccinations based on sub regions


## No. of safety side effects based on sub region


## days in regios where vaccination in that region was gretater than its daily average

with cte as (
SELECT avg(sni_covid19_vaccination) as avg_vaccination,sub_region_1 FROM `bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights` group by(sub_region_1)
)
SELECT maintable.sub_region_1, date  ,avg(sni_covid19_vaccination)as avgs  FROM `bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights`as maintable
join cte
 on maintable.sub_region_1=cte.sub_region_1
 WHERE sni_covid19_vaccination >=avg_vaccination 
 group by sub_region_1,date
 
 ![4](https://user-images.githubusercontent.com/88762643/131230081-a966bfa4-a6d9-4808-93a5-06547a192d0b.PNG)


