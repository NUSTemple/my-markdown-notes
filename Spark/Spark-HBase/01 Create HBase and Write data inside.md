
> Below commands will create a new namespace `eng_hbase_table_sales` and table `records` in the HBase with column family `cf`

```bash
create_namespace "eng_hbase_table_sales"
create "eng_hbase_table_sales:records", "cf"
```
