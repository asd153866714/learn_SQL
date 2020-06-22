# SELECT查詢指令

```
SELECT 欄位清單  
FROM 資料表來源 
[WHERE 搜尋條件] 
[GROUP BY 欄位清單] 
[HAVING 搜尋條件] 
[ORDER BY 欄位清單] 
```

* 查詢結果如果需要顯示資料表的所有欄位， SELECT指令可以直接使用 * 符號代表資料表的所有欄位。 

查詢書籍資料表中所有欄位的資料： 
```
SELECT *
FROM 書籍
```

```
SELECT 書籍名稱, CAST(價格 * 0.8 AS numeric(4, 0)) AS 折扣
FROM 書籍
```

```
SELECT TOP 2 *
FROM 書籍
```

```
SELECT TOP 30 PERCENT *
FROM 書籍
```

```
SELECT IDENTITYCOL, ROWGUIDCOL
FROM 書籍
```

```
SELECT DISTINCT 出版公司
FROM  書籍
```

```
SELECT TOP 3 WITH TIES *
FROM 書籍
ORDER BY 價格
```

```
SELECT 書籍名稱 AS 電腦書籍名稱
FROM 書籍
```

```

```
