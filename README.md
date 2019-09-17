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

## [IOT]

+ wifi | 蜂窝网络：[组网NSA](https://blog.csdn.net/liuyukuan/article/details/90641088) 

  蜂窝网络中一个基站（路由、网关）的覆盖范围为六角形；相邻六边形之间信号频率不同（防止发生信号间的相互干扰）；5G网络可以复用部分4G基站，以半自组网的方式完成覆盖（？2-》3-》4G转换的完成时间和方式）；？蜂窝网络和wifi只是通信协议不同（wuxi-free与4G在虹桥车站连接问题）；
  
  + ？5G 150倍能力提升的方式
  + ？分布式和harmonyOS的关键操作及其在5G竞争中的作用
  
+ 通信协议 ：标准的具体内容是什么，不同通信协议的区别、存在的必要性

+ 覆盖范围： （除了组网设计之外，通信领域应该考虑的）频率 分贝（db,信号强度）。 

+ 长连接 功耗 ：瓶颈是电池， apple watch做到了18小时（和移动电源一起）

+ 传感器网络

+ 可视化能够辅助解决的问题 ：信号覆盖测试和建模问题 ？

## 分布式

+ 微内核
+ docker实现隔离网络带宽和内存带宽
+ 分布式数据存储计算方案
+ ? 分布式.的代理服务器 [tengine](https://github.com/alibaba/tengine) 
+ ？引擎

## 设计原则

+ [面向对象](https://segmentfault.com/a/1190000020319171#articleHeader7) 还不是很会用的样子，部分参考活动节点建模
+ 依赖注入
+ 控制反转
+ 反向代理
+ 负载均衡

## KG 

异构数据融合 -》 高维特征建模和降维

维度建模过程 : 指标量化 -》 协方差矩阵 -》PCA主成分分析等降维方式 -> 补充/预估（批次质量测算结果）业务应用

高维度数据可视化方式： 点云形式表示的知识图谱（图数据库做输入数据和中间计算结果存储）.元数据完成数据源追溯

+ [基于知识图谱的小微企业贷款申请反欺诈](https://flashgene.com/archives/63679.html) 中国建设银行，201909
主要是（企业）节点、（干系人\亲属\担保）关系 表示和无关节点规约细节中有些不同。另外，试验部分要参考的一些点：
	
  + 图数据操作分析：neo4j + python igraph/networkX
  + 机器学习预排序算法：？_决策树系列的 xgboot，lightGBM 等_ 完全没有看懂过
  + 考虑数据特征的非独立同分布问题（节点标签信息可能影响其他节点） 

+ [Combining Latent Factor Model with Location Features for Event-based Group Recommendation](https://weizhangltt.github.io/paper/zhang-kdd2013.pdf) Tsinghua 2013

改进矩阵因子化方法和链路预测方法，完成POI(兴趣点）推荐. 另：event-based social network

  + 矩阵特征分解 ： 区别于betweeness等衡量结构上的直接连接关系强弱的指标。矩阵数值代表节点社群归属度(隐含的关联关系)，通过用户-组标签间的语义（NLP）相似性量化。
  
       
       Mij = Sim(useri,groupj) , sim():Jaccard similarity等语义相似度计算方法用在二者所带标签中
  + 改进版 Pairwise TagenhAnced and featuRe-based Matrix factorIzation for Group recommendAtioN (PTARMIGAN)

      tensor factorization需要的关系形式 <user, group, tag>

      ...三元组获取方式...

      后使用SGD进行参数学习

  + 实现细节：1. google geoCodimg ApI 完成距离计算
  
+ Temporal + Spatial [stanford2011](https://cs.stanford.edu/people/jure/pubs/mobile-kdd11.pdf)

+ [Event-based social networks: Linking the online and offline social worlds](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.649.2904&rep=rep1&type=pdf),KDD 2012 information diffusion 信息扩散, 基于事件的异构网络

  + 实现细节：
  
   1. ~~数据集~~
   
   2. 冷启动问题：设计异构EBSN信息流动（消息传播）模式.该模式应当考虑社区结构.，i.e. We design a number of diffusion patterns that capture the information flow over heterogenous Event-Based Social Network. Through experiments we demonstrate that the diffusion pattern that takes the community structures into account yields the best prediction power.

     - 基于事件及社区的传播模型：三种基本传播结构

       单道 U - G_online - U, U - G_offline - U ； 级联 U -G - G -U; 并发 U - G_online,G_offline - U

   3. event-based services: 

	- 事件定义：用户定义：（when, where, what,(permitted users)）

	- 事件触发：其他用户选择加入意愿 (yes, no, maybe)

   4. ESBN,网络定义：G = （Vertices_users, Arc_online_social_interactio,  Arc_offline_social_interaction）特点：融合线上（follow）和线下(attend, 带有location信息)的活动

   5. 实验部分
	- 统计方法分析了样本分布。数据呈现方式：normalized frequency等是很有意思的
	
	- 聚类(cluster)方法 -根据应用场景设置了目标函数；通过standard Davies-Bouldin 指标优化K（cluster大小）值选定

+ [Effective Community Search over Large Spatial Graphs](http://www.vldb.org/pvldb/vol10/p709-fang.pdf) 莳萝/地理社交网络 location-based social network

    （1）同时考虑结构内聚性（CD），空间内聚性(Approximation)，考虑位置移动实时在线计算社群（2）使用基于链接的社群发现方法，不使用图聚类（3）不使用索引结构保存子图结构等中间计算结果

    + 数据集 SNAP [loc-Brightkite](http://snap.stanford.edu/data/loc-Brightkite.html)
    + 考虑空间内聚性
    
     - geo-social network graph G = ( V , G )
     
    + CD方法
    
     - 综述1 ：2004, 1W+ [Finding and evaluating community struture in networks](http://www.cse.cuhk.edu.hk/~cslui/CMSC5734/newman_community_struct_networks_phys_rev.pdf)
     
      * 图分区 ： 并行计算中需要考虑的进程(process)-通信表征为网络节点-边，以平衡处理器负载 + 最小化边数量 （NP,有启发式算法）
      * 定义网络社区 ：Fig1
      * 层次聚类 ： 常用于社会学分析  ？_hjq sjtu_
           
	 分为凝聚类(agglomerative) 和 消除类（divisive）
        
	 ？层次树形成很像知识图谱的概念层：越高的层次包含越多的信息

     * 本文在undirected, unweighted网关注消除类（divisive）方法
      + 删除关联度最弱的关联，指标：
	1. 介数中心度 betweeness
	2. 电流电阻中心度量 current-flow betweeness recalculation √
      + 在电阻网络中的应用：
        1. 最短路径相关性
        2. 随机游走
      + 量化CD产生的社区结构内聚性：模块度
      + 数据集

## 过程管控

（内）企业信息系统内部过程管控

（外）供应链管控+（区块链）去中心化

应用中基础设施performance要求： 通过 distributed 降低 latency 。硬件的部分交给 ?FPGA

## TOdo

如何隔离内存和网络带宽？

亚美利剑 的Iot的研究点

蜂窝网与[资源配置]：(http://tow.cnki.net/kcms/detail/detail.aspx?filename=1019650209.nh&dbcode=CRJT_CDFD&dbname=CDFD2019&v=)

