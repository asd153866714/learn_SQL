# 建立資料庫

請指定資料檔和交易記錄檔的規格清單來建立名為【學校】 的資料庫，檔案是位在「C:\Data」路徑，如下所示： 

```
CREATE DATABASE 學校
ON PRIMARY   
( NAME='學校',
  FILENAME= 'C:\Data\學校.mdf',    
  SIZE=8MB,    
  MAXSIZE=10MB,    
  FILEGROWTH=1MB ) 
LOG ON   
( NAME='學校_log',    
  FILENAME = 'C:\Data\學校_log.ldf', 
  SIZE=1MB,     
  MAXSIZE=10MB,   
  FILEGROWTH=10% ) 
```

# 建立多檔案群組的資料庫

內含2個檔案群組、3 個資料檔和1個交易記錄檔，如下所示：

```

CREATE DATABASE 代理產品 
ON PRIMARY   
( NAME='代理產品',    
  FILENAME= 'C:\Data\代理產品.mdf',  
  SIZE=8MB,    
  MAXSIZE=10MB,   
  FILEGROWTH=1MB ), 
FILEGROUP 代理產品_群組
( NAME = '代理產品_群組_11',    
  FILENAME = 'C:\Data\代理產品_群組_11.ndf',  
  SIZE = 2MB,     
  MAXSIZE=10MB,    
  FILEGROWTH=1MB ),   
  ( NAME = '代理產品_群組_12',    
  FILENAME = 'C:\Data\代理產品_群組_12.ndf',
  SIZE = 2MB,    
  MAXSIZE=10MB,  
  FILEGROWTH=1MB ) 
LOG ON   
( NAME='代理產品_log',    
  FILENAME = 'C:\Data\代理產品_log.ldf', 
  SIZE=1MB,    
  MAXSIZE=10MB,
  FILEGROWTH=10% )
```

# 修改資料庫

* 使用ALTER DATABASE

* 在【產品】資料庫的【產品_群組】檔案群組，新 增名為【產品_群組_13】的資料檔，如下所示： 

```
ALTER DATABASE 產品 ADD FILE 
( NAME = '產品_群組_13',    
  FILENAME = 'C:\Data\產品_群組_13.ndf', 
  SIZE = 2MB,   
  MAXSIZE=10MB,    
  FILEGROWTH=1MB ) TO FILEGROUP 產品_群組 
```

* 請在【產品】資料庫新增名為【產品_log2】的交 易記錄檔，如下所示： 

```
ALTER DATABASE 產品 ADD LOG FILE  
( NAME = '產品_log2',  
  FILENAME = 'C:\Data\產品_log2.ldf', 
  SIZE = 5MB,   
  MAXSIZE=10MB,  
  FILEGROWTH=1MB ) 
```

* 調整【代理產品】資料庫交易記錄檔案 的尺寸成為5MB，如下所示： 
```
ALTER DATABASE 代理產品 MODIFY FILE  
( NAME = '代理產品_log', 
  SIZE = 5MB ) 
```

* 更改【代理產品】資料庫預設檔案群組為 【代理產品_群組】，如下所示： 
```
ALTER DATABASE 代理產品 
MODIFY FILEGROUP 代理產品_群組
  DEFAULT
```

# 刪除使用者資料庫

刪除用 DROP :

`DROP DATABASE 資料庫名稱清單 `
