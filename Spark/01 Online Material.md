# Online Material

1. [Spark:Case 6: Reading Data from HBase and Writing Data to HBase](https://forum.huawei.com/enterprise/en/Spark-Case-6-Reading-Data-from-HBase-and-Writing-Data-to-HBase/thread/469231-899)

2. [Spark 读写 HBase 的两种方式（RDD、DataFrame） - 伏天氏 - CSDN博客](https://blog.csdn.net/yitengtongweishi/article/details/82556824)

3. [HBase读写的几种方式（二）spark篇 - 牧梦者 - 博客园](https://www.cnblogs.com/swordfall/p/10517177.html)

4. [Efficiently read HBase records without schema in Spark? - Hortonworks](https://community.hortonworks.com/questions/108604/efficiently-read-hbase-records-without-schema-in-s.html)
```scala
val sc=new Scan()
// add two filters in filterlist (keyonlyfilter,firstkeyonlyfilter)
// add that filterlist to scan
val conf =HBaseConfiguration.create()
conf.addResource(newPath("hbase-site.xml"))
conf.set("hbase.zookeeper.quorum","xxx")
conf.set(TableInputFormat.INPUT_TABLE,"TEST_TABLE")
conf.set(TableInputFormat.SCAN,convertscantoString(sc))
val hBaseRDD = sc.newAPIHadoopRDD(conf, 
classOf[org.apache.hadoop.hbase.mapreduce.TableInputFormat], 
classOf[org.apache.hadoop.hbase.io.ImmutableBytesWritable], 
classOf[org.apache.hadoop.hbase.client.Result])
hBaseRDD.count()
```

5. [Insert Spark dataframe into hbase](https://stackoverflow.com/questions/44111988/insert-spark-dataframe-into-hbase#44113523)

