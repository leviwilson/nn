## Newznab Scripts / Info

### Database Size
```sql
SELECT  table_schema "Data Base Name",
        sum( data_length + index_length ) 1024 /  1024 "Data Base Size in MB",
        sum( data_free )/ 1024 / 1024 "Free Space in MB"
FROM information_schema.TABLES  GROUP BY table_schema;
```

### Post-Processing Info
```sql
select (select count(*) from binaries) as Binaries,
(select count(*) from parts) as Parts,
(select count(*) from releases where passwordstatus<0) as PwdCheck,
(select count(*) from releases where bookinfoID is null and categoryID=7020) as BookLookups,
(select count(*) from releases where consoleinfoID is null and categoryID between 1000 and 1999) as ConsoleLookups,
(select count(*) from releases where musicinfoID is null and categoryID between 3000 and 3999) as MusicLookups,
(select count(*) from releases where imdbID is null and categoryID between 2000 and 2999) as MovieLookups,
(select count(*) from releases where rageID is null and categoryID between 5000 and 5999) as TVLookups,
(select count(*) from releases where nfostatus<0) as NFOlookups,
(select count(*) from releases) as Releases;
```
