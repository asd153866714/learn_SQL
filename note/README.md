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
