2 分析如下HiveQL，生成的MapReduce执行程序，map函数输入是什么？输出是什么，reduce函数输入是什么？输出是什么？
INSERT OVERWRITE TABLE pv_users
SELECT pv.pageid, u.age
FROM page_view pv
JOIN user u
ON (pv.userid = u.userid);

![](https://wx2.sinaimg.cn/mw690/6a8f9c5bly1gi35ji9hasj214c087ab2.jpg)

