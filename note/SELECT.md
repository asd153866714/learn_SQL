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

# JOIN
* JOIN 的意義是將多個資料表的記錄橫向連接起來, 然後利用 ON 來設定條件以過濾不需要的記錄。

```
SELECT	企劃書籍.編號, 名稱, 價錢
FROM	企劃書籍 JOIN 企劃書籍預定價
	ON 企劃書籍.編號 = 企劃書籍預定價.編號
```

## INNER JOIN
查詢兩家公司有那些共同的產品及產品的價格：
```
SELECT	旗.產品名稱 AS 旗旗公司產品名稱, 旗.價格, 
	標.產品名稱 AS 標標公司產品名稱, 標.價格
FROM	旗旗公司 AS 旗 JOIN 標標公司 AS 標
	ON 旗.產品名稱 = 標.產品名稱
```

## LEFT JOIN
找出兩家公司共同的產品及價格, 以及旗旗公司的獨家產品：
```
SELECT	旗.產品名稱 AS 旗旗公司產品名稱, 旗.價格, 
	標.產品名稱 AS 標標公司產品名稱, 標.價格
FROM	旗旗公司 AS 旗 LEFT JOIN 標標公司 AS 標
	ON 旗.產品名稱 = 標.產品名稱
```

## RIGHT JOIN
查詢兩家公司共同的產品和價格, 以及標標公司有什麼獨家產品：
```
SELECT	旗.產品名稱 AS 旗旗公司產品名稱, 旗.價格, 
	標.產品名稱 AS 標標公司產品名稱, 標.價格
FROM	旗旗公司 AS 旗 RIGHT JOIN 標標公司 AS 標
	ON 旗.產品名稱 = 標.產品名稱
```

## FULL JOIN
查詢兩家公司所有的產品和價格：
```
SELECT	旗.產品名稱 AS 旗旗公司產品名稱, 旗.價格, 
	標.產品名稱 AS 標標公司產品名稱, 標.價格
FROM	旗旗公司 AS 旗 FULL JOIN 標標公司 AS 標
	ON 旗.產品名稱 = 標.產品名稱
```

## CROSS JOIN
 將兩家公司的每項產品一一比對：
```
SELECT  旗.產品名稱 AS 旗旗公司產品名稱, 旗.價格, 
	標.產品名稱 AS 標標公司產品名稱, 標.價格
FROM	旗旗公司 AS 旗 CROSS JOIN 標標公司 AS 標
```

## Self-Joins
* 有時候我們會將同一個資料表自己 JOIN 自己, 例如在員工資料表中, 每個人都有一個主管編號欄來 存放其主管的編號： 

查詢每位員工的姓名、職位、及其主管姓名：
```
SELECT  員工.姓名, 員工.職位,
        長官.姓名 AS 主管
FROM	員工 LEFT JOIN 員工 AS 長官
	ON 員工.主管編號 = 長官.編號
```

# WHERE 子句
* WHERE 子句用來設定查詢的條件

從員工資料表中, 找出女性員工的資 料, 就可以寫成：
```
SELECT	*
FROM	員工
WHERE	性別 = '女'
```

# GROUP BY 子句 
* GROUP BY 子句可將資料列依據設定的條件, 分成數個群組, 並且讓 SELECT 子句中所使用的彙總函數 ( SUM、 COUNT、MIN、MAX 、AVG ...)產生作用。

* 在 SELECT 子句的欄位列表中, 除了彙總函數外, 其它所出現的欄位一定要在 GROUP BY 子句中有 定義才行。例如 "GROUP BY A, B", 那麼 "SELECT MAX(A), C" 就有問題, 因為 C 不在 GROUP BY 中, 但 MAX(A) 還是可以的

* GROUP BY 子句中不能使用欄位別名。

從出貨記錄資料表中查詢出貨給各家客戶的總數量時, 可用 GROUP BY 子句將出貨記錄資料表的記錄按客戶名稱分組來計算： 
```
SELECT		客戶名稱, SUM(數量) AS 出貨數量
FROM		出貨記錄
GROUP BY	客戶名稱
```

## CUBE：對所有欄位加總運算 
* CUBE 參數會自動對 GROUP BY 所列的分組欄 位做加總運算。
```
SELECT	客戶名稱, 書名, SUM(數量) AS 出貨數量
FROM	出貨記錄
GROUP BY CUBE	(客戶名稱, 書名)
```

## ROLLUP：對第一個欄位加總運算 
* ROLLUP 只會依據 GROUP BY 子句所列的第一 個欄位做加總運算。
```
SELECT	客戶名稱, 書名, SUM(數量) AS 出貨數量
FROM	出貨記錄
GROUP BY ROLLUP	(客戶名稱, 書名)
```

# HAVING 子句
* HAVING 子句也可以設定查詢的條件, 但一般會和 GROUP BY 子句搭配使用。 
* 如果查詢中沒有使用 GROUP BY 子句, 則 HAVING 子句的用途和 WHERE 子句的用途相似, 不過 HAVING 子句和 WHERE 子句還是有差別的, 即彙總函數無法在 WHERE 子句中使用, 只能用在 HAVING 子句中。 

從出貨記錄資料表中查詢, 哪一本書進 書總量超過 6 本, 以及是哪家書店進的：
```
SELECT	客戶名稱, 書名, SUM(數量) AS 總數量
FROM	出貨記錄
ORDER BY 客戶名稱, 書名
HAVING SUM(數量) >= 6
```
<br>
用 HAVING 條件來選出 COUNT 大於 1 的記錄： 
```
SELECT	客戶名稱, 書名, SUM(數量) AS 總數量
FROM	出貨記錄
ORDER BY 客戶名稱, 書名
HAVING COUNT(*) > 1
```

# ORDER BY 子句 
* ASC：以升冪方式 (由小而大) 的方式排序, 這是預設的排序方式。 
* DESC：以降冪方式 (由大而小) 的方式排序。 

以客戶名稱做降冪排序, 而客戶名稱 相同的資料再以數量做升冪排序： 
```
SELECT *
FROM 出貨記錄
ORDER BY 客戶名稱 DESC, 數量 ASC
```

# COMPUTE 子句 
* COMPUTE 可做分組小計, 它可以將資料表的記錄依指定的欄位歸類, 每一類產生一或多個加總、平均 ... 等計算值。

顯示出貨記錄資料表中所有的出貨記 錄, 以及總出貨量：
```
SELECT	*
FROM	出貨記錄
ORDER BY 客戶名稱
COMPUTE SUM(數量) BY 客戶名稱
```
