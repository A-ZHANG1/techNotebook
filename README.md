# 小本本

学习如何做一个技术人. 参考[策女神](https://github.com/dyweb/papers-notebook)的论文阅读笔记和[航天](./航天数仓相关笔记.md)的技术笔记. [Markdown](https://www.jianshu.com/p/335db5716248).

## 大蛇

### 逼格Data
+ TDH操作流程

  oracle  --  sqoop（select语句） -->  hdfs
 
           -- 连接hive（beeline） -->  hive
           
              建表(create table)
              
              加载数据(load)
          
          --> ... inceptor 
  

                             
                
+ 工作流引擎：workflow

+ 星环其他技术工具

  流上的数据挖掘： slipstream:  在流上构建复杂应用 高可用性和exactly-one语义 机器学习可运行在事件驱动的流引擎上


### Django

### 数据分析

### 深度有趣

## sql

### Oracle操作plsql一些基本的数据检视操作：

+ SELECT DISTINCT(col_name) FROM table_name T
+ SELECT (col_name),COUNT(*) FROM table_name T GROUP BY col_name
+ SELECT COUNT(col_name1),COUNT(col_name2) FROM table_name T
+ subquery解决合并的table的子查询: select count(*) from (select distinct col1, col2 from mytable);

基本的检视和清洗也可以考虑在数据库中做，也可以考虑抽取出来之后做

## [Java和算法的每日刷题](https://github.com/A-ZHANG1/Exercise-Book)

## [社团发现]

+ [tsinghua2016](http://www.cnki.com.cn/Article/CJFDTOTAL-QHXB201710004.htm) 基于Spark的并行增量动态社群发现算法 [also in zotero]
  基于Spark GraphX的并行增量动态社群发现算法PIDCDS：根据上一时刻网络结构，计算当前时刻增量节点的社群归属，其他节点社群归属保持不变，保持了网络界都变化的短时平滑性，比FaceNet更加稳定。
  
+ [社群发现研究进展](https://cloud.tencent.com/developer/article/1188299) 
  腾讯171023的技术文，不同的方法和研究方向


## TDH
workflow : 10.123.195.8:9091 用户名:workflow 密码:Transwarp4T
           extract_data 脚本获取
```shell
cd /var/lib/workflow2/TDH-Client
source init.sh
export HADOOP_USER_NAME=hdfs

hadoop fs -ls /tmp/sqoop
#hadoop fs -echo
#显示数据行数
hadoop fs -cat /inceptor1/user/hive/warehouse/original.db/hive/twoscreening | wc -l
hadoop fs -cat /tmp/sqoop/shells/twoscreening.sh
```







