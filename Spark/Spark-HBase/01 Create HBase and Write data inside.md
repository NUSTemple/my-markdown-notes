
> Below commands will create a new namespace `eng_hbase_table_sales` and table `records` in the HBase with column family `cf` in **`hbase shell`**

```bash
# Below commands are issued in hbase shell
create_namespace "eng_hbase_table_sales"
create "eng_hbase_table_sales:records", "cf"
```



Download a sample dataset online

I downloaded this structured sales transaction data from [data down link](http://eforexcel.com/wp/wp-content/uploads/2017/07/1500000%20Sales%20Records.zip) . This contains 1.5 million records

Then the here is the sample code to write data into HBase by Spark

[SparkHBaseWriterTemplate](https://github.com/NUSTemple/hbase-reader/blob/master/src/main/scala/com/micron/f10ds/SparkHBaseWriterTemplate.scala)

Key Code Snippet

```scala
t.foreachPartition { iter =>
    // Create HBase Connection
        val hbaseConf = HBaseConfiguration.create()
        hbaseConf.addResource("file:///home/pengtan/Downloads/hbase-site.xml")
        hbaseConf.set("hbase.zookeeper.quorum","master01,slave01,slave02")
        hbaseConf.set("hbase.zookeeper.property.clientPort", "2181")

        hbaseConf.set("hbase.master", "192.168.1.169:16000")
        hbaseConf.set("zookeeper.session.timeout", "300000")
        hbaseConf.set("zookeeper.znode.parent", "/hbase-unsecure")
        hbaseConf.set(TableOutputFormat.OUTPUT_TABLE, tableName)

        val connection = ConnectionFactory.createConnection(hbaseConf)

        val table = connection.getTable(TableName.valueOf(tableName))
        iter.foreach { a =>


          val arr = a.split(",")
    // Add columns into Put
          val p = new Put(Bytes.toBytes(arr(rowkeyIndex)))
          for (i <- headers.indices ) {
            p.addColumn(Bytes.toBytes(cfamily), Bytes.toBytes(headers(i)), Bytes.toBytes(arr(i)))
          }
          table.put(p)
        }
    }
```

