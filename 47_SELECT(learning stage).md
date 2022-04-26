## 47 (NEW)

Определить страны, которые потеряли в сражениях все свои корабли.

```sql
WITH All_ships AS (
    SELECT c.country, s.name
    FROM ships s JOIN classes c ON s.class=c.class
    UNION
    SELECT c.country, o.ship 
    FROM outcomes o JOIN classes c ON c.class=o.ship
)
SELECT DISTINCT country FROM All_ships
WHERE country NOT IN (
 SELECT country FROM All_ships
 WHERE All_ships.name NOT IN ( SELECT ship name FROM outcomes WHERE 
  result = 'sunk')
)
```
