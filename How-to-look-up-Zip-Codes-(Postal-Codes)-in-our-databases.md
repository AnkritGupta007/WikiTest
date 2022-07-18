# Zip Code in Databases
Here at CMU we have good lookup data on zip codes that can be found in:
**Server**: `IT-WebDB`
**Databse**: `Pros_ZipCodes`

```sql
-- example query
SELECT *
  FROM [Pro_ZipCodes].[dbo].[ZIPCodesRawData]
  Where ZipCode = '48858'
```

## Tags
[[Database]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DatabaseTag)