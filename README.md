# SQLServer
### Last Login User
```sql
SELECT DatabaseName, MAX(LastAccessDate) LastAccessDate

FROM
    (SELECT
        DB_NAME(database_id) DatabaseName
        , last_user_seek
        , last_user_scan
        , last_user_lookup
        , last_user_update
    FROM sys.dm_db_index_usage_stats) AS PivotTable

UNPIVOT 

    (LastAccessDate FOR last_user_access IN
        (last_user_seek
        , last_user_scan
        , last_user_lookup
        , last_user_update)
    ) AS UnpivotTable

GROUP BY DatabaseName

HAVING DatabaseName NOT IN ('master', 'tempdb', 'model', 'msdb')

ORDER BY 2
```

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
