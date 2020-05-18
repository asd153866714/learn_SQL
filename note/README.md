# 建立資料庫

請指定資料檔和交易記錄檔的規格清單來建立名為【學校】 的資料庫，檔案是位在「C:\Data」路徑，如下所示： 

```SQL
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

```SQL

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
