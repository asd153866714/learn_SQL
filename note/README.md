```
CREATE DATABASE 學校 ON PRIMARY   ( NAME='學校',     FILENAME= 'C:\Data\學校.mdf',     SIZE=8MB,     MAXSIZE=10MB,     FILEGROWTH=1MB ) LOG ON   ( NAME='學校_log',     FILENAME = 'C:\Data\學校_log.ldf',     SIZE=1MB,     MAXSIZE=10MB,     FILEGROWTH=10% ) 
```
