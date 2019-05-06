# SQLServer
### Foreign keys
Find foreign keys:
```sql
 EXEC sp_fkeys @pktable_name = N'Tablename' ,@pktable_owner = N'dbo'
 ```
 > Note: you should choose the table that hosts the foreign key, not the table where it is applied.
 
 Add foreign key:
 ```sql
ALTER TABLE scheme.TableName
ADD FOREIGN KEY (ColumnName) 
REFERENCES scheme.SourceTableName(ColumnName)
```
