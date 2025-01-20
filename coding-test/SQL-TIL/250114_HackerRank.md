# HackerRank 

- 푼 일자: 2025년 1월 14일 
- Easy 레벨 총 10개

### 풀이

- `UNION` 사용해서 쿼리 합치기

```sql
# Weather Observation Station 5
(SELECT city, LENGTH(city) FROM station ORDER BY LENGTH(city), city LIMIT 1)
UNION
(SELECT city, LENGTH(city) FROM station ORDER BY LENGTH(city) DESC, city LIMIT 1);
```