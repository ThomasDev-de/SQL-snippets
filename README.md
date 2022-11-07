# SQL-snippets

A collection of useful SQL snippets  

## Time period checks
```sql
SELECT * FROM table_events
```

| id  | title   | start               | end                 |
|-----|---------|---------------------|---------------------|
| 1   | Event 1 | 2022-10-31 10:00:00 | 2022-10-31 12:00:00 |
| 2   | Event 2 | 2022-10-31 13:00:00 | 2022-10-31 14:00:00 |
| 3   | Event 3 | 2022-10-31 15:00:00 | 2022-10-31 16:00:00 |
| 4   | Event 4 | 2022-11-01 15:00:00 | 2022-11-01 16:00:00 |


### Check if a time period does `not intersect` other time periods

```sql
SET @start = "2022-10-31 10:00:00";
SET @end = "2022-10-31 12:00:00";

SELECT id FROM `table_events`
WHERE 
    (`start` < @start AND `end` < @start)
AND (`start` > @end)
```
### Check if a time period intersects other time periods
```sql
SET @start = "2022-10-31 10:00:00";
SET @end = "2022-10-31 12:00:00";

SELECT id FROM `table_events`
WHERE 
    NOT(
            (`start` < @start AND `end` < @start)
        AND (`start` > @end)
    )
```