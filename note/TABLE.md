# 資料表的建立 

在【教務系統】資料庫新增【教授】資料表，且 新增自動編號的【建檔編號】欄位，如下所示： 

```
CREATE TABLE 教授 (    
  建檔編號   int         IDENTITY(1000, 1),
  教授編號   char(4)     NOT NULL PRIMARY KEY, 
  職稱       varchar(10), 
  科系       varchar(5),
  身份證字號 char(10)   NOT NULL 
 ) 
```

### 計算欄位

* 計算欄位（Computed Columns）是一種沒有儲 存值的資料表欄位，它的值是使用同一筆記錄其 他欄位建立的運算式計算而得。
  
  * 在Management Studio新增計算欄位就是在 編輯畫面下方指定【計算資料行規格/公式】 的欄位屬性。

  * T-SQL指令是使用AS關鍵字來指定計算欄位的運算式
  
在【教務系統】資料庫新增【估價單】資料表， 最後的【平均單價】欄位是一個計算欄位，其運 算式為【總價 / 數量】，如下所示： 
```
CREATE TABLE 估價單 (    
  估價單編號  int    NOT NULL IDENTITY PRIMARY KEY,    
  產品編號    char(4)  NOT NULL,    
  總價        decimal(5, 1) NOT NULL,    
  數量        int       NOT NULL DEFAULT 1,    
  平均單價    AS  總價 / 數量 
) 
```

### 疏鬆欄位

* 疏鬆欄位必須大部分記錄的欄位值為NULL值。

* 疏鬆欄位不能作為主鍵欄位，也不可以用來建立 叢集索引。 

  • 在Management Studio新增疏鬆欄位就是在 編輯畫面下方的【為疏鬆】欄位，將屬性 值改為【是】。 
  • T-SQL指令是使用SPARSE關鍵字來指定 欄位為疏鬆欄位。 
