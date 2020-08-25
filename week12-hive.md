2 分析如下HiveQL，生成的MapReduce执行程序，map函数输入是什么？输出是什么，reduce函数输入是什么？输出是什么？
INSERT OVERWRITE TABLE pv_users
SELECT pv.pageid, u.age
FROM page_view pv
JOIN user u
ON (pv.userid = u.userid);

![](https://wx2.sinaimg.cn/mw690/6a8f9c5bly1gi35ji9hasj214c087ab2.jpg)

mapreduce的过程，map阶段，从文件中读取数据，按照userid作为key进行划分，数据分片经过shuffle过程，作为reduce的输入，reduce阶段将数据进行拼接，输出到表的文件中。

