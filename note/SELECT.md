# SELECT 基本架構
```
SELECT 欄位清單  
FROM 資料表來源 
[WHERE 搜尋條件] 
[GROUP BY 欄位清單] 
[HAVING 搜尋條件] 
[ORDER BY 欄位清單] 
```

# SELECT 子句
* 查詢結果如果需要顯示資料表的所有欄位， SELECT指令可以直接使用 * 符號代表資料表的所有欄位。 

查詢書籍資料表中所有欄位的資料： 
```
SELECT *
FROM 書籍
```

查詢書籍資料表中書籍名稱欄位和價 格欄位的資料, 而且價格欄位的值還要打 8 折： 
```
SELECT 書籍名稱, CAST(價格 * 0.8 AS numeric(4, 0)) AS 折扣
FROM 書籍
```

顯示書籍資料表中出版公司欄位不重複的資料：
```
SELECT DISTINCT 出版公司
FROM  書籍
```

查詢書籍資料表的前 2 筆記錄： 
```
SELECT TOP 2 *
FROM 書籍
```

查詢書籍資料表的前 30% 的記錄： 
```
SELECT TOP 30 PERCENT *
FROM 書籍
```

WITH TIES 是平手的意思, 當要顯示的資料在排 序時有平手的狀況時, 則一併顯示出來：
```
SELECT TOP 3 WITH TIES *
FROM 書籍
ORDER BY 價格
```

從書籍資料表查詢具 備 IDENTITY 以及 RowGuid 屬性的欄位值： 
```
SELECT IDENTITYCOL, ROWGUIDCOL
FROM 書籍
```

用 AS 設定欄位別名：
```
SELECT 書籍名稱 AS 電腦書籍名稱
FROM 書籍
```

# FROM 子句
* FROM 子句的基本用法是設定要查詢的資料來源, 如資料表名稱、檢視表名。

我們以客當作客戶名稱資料表的別名, 以出當作出貨記錄資料表的別名：
```

```

# JOIN
* JOIN 的意義是將多個資料表的記錄橫向連接起來, 然後利用 ON 來設定條件以過濾不需要的記錄。

## INNER JOIN

## LEFT JOIN

## RIGHT JOIN

## FULL JOIN

## CROSS JOIN

## Self-Joins

# WHERE 子句 

# GROUP BY 子句 

## CUBE：對所有欄位加總運算 

## ROLLUP：對第一個欄位加總運算 


# 9-6 HAVING 子句 


# ORDER BY 子句 


# COMPUTE 子句 
