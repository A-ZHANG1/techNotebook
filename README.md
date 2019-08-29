# 小本本

学习如何做一个技术人. 参考[策女神](https://github.com/dyweb/papers-notebook)的论文阅读笔记和[航天](./航天数仓相关笔记.md)的技术笔记. [Markdown](https://www.jianshu.com/p/335db5716248).

## 大蛇

### 逼格Data

+ [TDH](https://www.bookstack.cn/read/HadoopAndSparkDataStudy/Content-3-chapter0303.md)操作流程

```
  oracle  --  sqoop（select语句） -->  hdfs
 
           -- 连接hive（beeline） -->  hive
           
              建表(create table)
              
              加载数据(load)
          
          --> ... inceptor 
```  

                             
                
+ 工作流引擎：workflow

workflow : 10.123.195.8:9091 用户名:workflow 密码:Transwarp4T
           extract_data 脚本获取
           
+ hdfs启动过程[shell command in linux]()

```shell
cd /var/lib/workflow2/TDH-Client
source init.sh
export HADOOP_USER_NAME=hdfs
```

+ [hadoop shell指令](http://hadoop.apache.org/docs/r1.0.4/cn/hdfs_shell.html)

```shell
#hadoop fs -echo
#显示数据行数
hadoop fs -cat /inceptor1/user/hive/warehouse/original.db/hive/twoscreening | wc -l
#打印文件内容
hadoop fs -cat /tmp/sqoop/shells/twoscreening.sh
#显示hdfs目录中的文件
hadoop fs -ls /tmp/sqoop/shells
#将脚本本地vim后放入hdfs
hadoop fs -copyFromLocal <localFile> <hdfs/directory>

hadoop fs -get <hdfs/directory1> <hdfs/directory2>

#修改shell
hadoop fs -text $1>hvim.txt
vim hvim.txt
hadoop fs -rm -skipTrash $1
hadoop fs -copyFromLocal hvim.txt $1
rm hvim.txt
hadoop fs -chmod 777 $1

```

+ 平台操作相关
```
#脚本文件放置路径
   ~/sqoop_import_shells/test_incremnent.sh

# terminal快捷操作
   command shift r 搜索最近使用的命令
   
   中间滚轴复制
```

+ shell基本常识:

  1. tab可联想补全
  2. 可以尝试用iterm2 + zsh做终极shell工具
  
```shell
vi filename
vim filename

```

+ 自动脚本...啊qsb

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







