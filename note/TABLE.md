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

  * 在Management Studio新增疏鬆欄位就是在 編輯畫面下方的【為疏鬆】欄位，將屬性 值改為【是】。 
  
  * T-SQL指令是使用SPARSE關鍵字來指定 欄位為疏鬆欄位。 
  
  在【教務系統】資料庫新增【廠商】資料表，最後的【分公司數】欄位是一個疏鬆欄位，因為大部分廠商都沒有分公司，如下所示：
  ```
  CREATE TABLE 廠商 (   
    廠商編號  int    NOT NULL IDENTITY PRIMARY KEY,     
    廠商名稱  varchar(100),    
    分公司數  int    SPARSE 
  ) 
  ```
  
### 建立PRIMARY KEY條件約束
  
在【教務系統】資料庫新增【訂單明細】資料表， 其主鍵是【訂單編號】和【項目序號】欄位的複合鍵，如下所示： 

```
CREATE TABLE 訂單明細 (    
  訂單編號   int       NOT NULL,     
  項目序號   smallint  NOT NULL,    
  數量       int       DEFAULT 1,    
  PRIMARY KEY (訂單編號, 項目序號) 
)
```

### 建立CHECK條件約束

* CHECK條件約束能夠限制欄位值是否在指 定的範圍，其內容是條件運算式，運算結果如為true，就允許存入欄位資料，否則不允許存入。 
```
[ CONSTRAINT 條件約束名稱 ] 
CHECK (條件運算式)
```

在【教務系統】資料庫新增【訂單】資料表，並且在【訂單總價】和【付款總額】欄位建立欄位層級的CHECK條件約束，如下所示： 
```
CREATE TABLE 訂單 (    
  訂單編號   int   NOT NULL IDENTITY PRIMARY KEY,     
  訂單總價   money NOT NULL         
    CONSTRAINT 訂單總價_條件約束        
    CHECK (訂單總價 > 0),    
  付款總額   money DEFAULT 0   
    CHECK (付款總額 > 0) 
)
```

```
CREATE TABLE 我的訂單 (    
  訂單編號   int   NOT NULL IDENTITY PRIMARY KEY,     
  訂單總價   money NOT NULL,    
  付款總額   money DEFAULT 0,    
    CHECK ( (訂單總價 > 0) AND (付款總額 > 0)              
      AND (訂單總價 > 付款總額)) 
) 
```

### 建立資料表的關聯性

在【教務系統】資料庫建立【班級】資料表，並且使用FOREIGN KEY條件約束，建立與【學 生】、【課程】和【教授】資料表的關聯性，如下所示：

```
CREATE TABLE 班級 (    
  教授編號   char(4)  NOT NULL,    
  課程編號   char(5)  NOT NULL,   
  學號       char(4)  NOT NULL               
    REFERENCES 學生 (學號),    
  上課時間   datetime,    
  教室       varchar(8),   
    PRIMARY KEY (學號, 教授編號, 課程編號),  
    FOREIGN KEY (教授編號) REFERENCES 教 授 (教授編號),   
    FOREIGN KEY (課程編號) REFERENCES 課 程 (課程編號) 
  ) 
```

# 修改與刪除資料表 

### 重新命名資料表 

* EXEC sp_rename '物件名稱', '新名稱' [,'物件型態'] 

`EXEC sp_rename '訂單', '學校訂單' `
  
### 修改資料表欄位

新增欄位
```
ALTER TABLE 我的訂單    
  ADD 訂單日期 datetime NOT NULL,         
  送貨日期 datetime 
```

刪除欄位
```
ALTER TABLE 我的訂單    
  DROP COLUMN 送貨日期 
```

更新欄位
```
ALTER TABLE 我的訂單    
  ALTER COLUMN 訂單日期 varchar(20) NOT NULL 
```

### 刪除資料表

`DROP TABLE 資料表名稱 `


