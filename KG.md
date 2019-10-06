## KG

### 基础知识

 - 属性图(property graph)

   * schema问题 [官方文档](https://s3.amazonaws.com/artifacts.opencypher.org/website/materials/sql-pg-2018-0056r1-Property-Graph-Schema.pdf)schema是什么，是对边条数，属性基数的约束。LPG是否需要schema,是。由于模式(schema)是非结构化的，定义图模型较为复杂。如果选择手动定义schema,如果需要大量定义的话可以想见这个工作是枯燥乏味的，于是有（半）自动生成的必要。

   * schema定义的方式：
   * 0. [schema抽取](https://nielsdejong.nl/projects/graph/schema-extraction-methodology.pdf) 
   * 1. 关联规则发现：[apriori算法](https://cloud.tencent.com/developer/article/1114170)产生的频繁项集合，作为关联规则，支持数据抽取
   * 2. 通过图模式[生成合成图数据](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.84.1081&rep=rep1&type=pdf)。

#### 1_图论 （静态图）

#### 2_网络动力学
1.基于时空特性
  + Temporal + Spatial [stanford2011](https://cs.stanford.edu/people/jure/pubs/mobile-kdd11.pdf)
  
  + [Effective Community Search over Large Spatial Graphs](http://www.vldb.org/pvldb/vol10/p709-fang.pdf) 莳萝/地理社交网络 location-based social network

    （1）同时考虑结构内聚性（CD），空间内聚性(Approximation)，考虑位置移动实时在线计算社群（2）使用基于链接的社群发现方法，不使用图聚类（3）不使用索引结构保存子图结构等中间计算结果

    + 数据集 SNAP [loc-Brightkite](http://snap.stanford.edu/data/loc-Brightkite.html)
    + 考虑空间内聚性
    
     - geo-social network graph G = ( V , G )
     
    + [CD]()方法
    
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

2.事件触发
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

### 研究方向

#### 数据融合

1. 基于概率的知识融合 [Google KDD14](https://www.cs.ubc.ca/~murphyk/Papers/kv-kdd14.pdf)
2. 异构数据融合 -》 高维特征建模和降维
  + 维度建模过程 : 指标量化 -》 协方差矩阵 -》PCA主成分分析等降维方式 -> 补充/预估（批次质量测算结果）业务应用
  + 高维度数据可视化方式： 点云形式表示的知识图谱（图数据库做输入数据和中间计算结果存储）.元数据完成数据源追溯
3. 数据资源管理细节
  + 。。。
  
#### 图query

#### 图分析

2. embedding
  * sensor embedded networks[传感器网络](https://pdfs.semanticscholar.org/9758/756853d77f31de6df78130c295b49e9699a1.pdf)

+ [Combining Latent Factor Model with Location Features for Event-based Group Recommendation](https://weizhangltt.github.io/paper/zhang-kdd2013.pdf) Tsinghua 2013

改进矩阵因子化方法和链路预测方法，完成POI(兴趣点）推荐. 另：event-based social network

  + 矩阵特征分解 ： 区别于betweeness等衡量结构上的直接连接关系强弱的指标。矩阵数值代表节点社群归属度(隐含的关联关系)，通过用户-组标签间的语义（NLP）相似性量化。
  
       
       Mij = Sim(useri,groupj) , sim():Jaccard similarity等语义相似度计算方法用在二者所带标签中
  + 改进版 Pairwise TagenhAnced and featuRe-based Matrix factorIzation for Group recommendAtioN (PTARMIGAN)

      tensor factorization需要的关系形式 <user, group, tag>

      ...三元组获取方式...

      后使用SGD进行参数学习

  + 实现细节：1. google geoCodimg ApI 完成距离计算
  
#### 知识图谱可视化：
   * 1.用于事件流监测
   * 2. 多维标度(multi-dimensional scaling)图中，基于几何推理的异常点监测和过滤技术。,优化嵌入质量
   * 3. 可视化辅助完成HIS系统中text-based本体生成：[SNIK 2019](http://ebooks.iospress.nl/publication/52489) 
      - 文本读取知识到预定义csv的CSV列中
      - csv被表征为RDF形式，画入sink知识图中
      - [知识图](http://www.snik.eu/graph/)中的不同颜色聚类(5 colored clouds)代表从不同书中获取的知识
      - 4个不同的RDF描述的[subontology](https://github.com/IMISE/snik-ontology)，分为hand-crafted/另3个数据源。[ontology schema](https://github.com/IMISE/snik-ontology/blob/master/meta.rdf)  
   * 4.schema.csv上传实例层可视化 [sb+vue+d3](https://github.com/MiracleTanC/Neo4j-KGBuilder)  [python](https://github.com/liuhuanyong/LanguageKnowledgeGraph/tree/master/web_law)，贝格佳卉做的元数据上传-》本体属性融合建模-》实例上传-》包络分析等数据可视化分析Demo
   * 5.[Harvard extension CS171](https://www.cs171.org/2015/assets/slides/11-graphs.pdf)  [graph visualization ppt] http://www.cs171.org/2018/
     
#### 图特征融合和计算
1. [主动的知识图谱特征混合](https://www.kde.cs.uni-kassel.de/wp-content/uploads/atzmueller/paper/2017-atzmueller-kcap.pdf)。通过形式化的方式,完成交互式的半自动架构，支持特征工程(可以后续改变schema,从而知识获取；可支持数据溯源)
  + 知识图谱中的可视化对象：
    1. 整体的图形化的网络结构 [12]
    2. 密集的连接子图(社群) [11]
    3. 特殊的集群 [8]
    4. 特征对矩阵 [本文]
  + 方法细节：
    1. 蓝色区域为带有该特征的样本数量的热力图
    2. 黄色（对角线）上是该特征本身的描述
    3. 灰色区域为两个特征间的相关性分析（过高相关性的两个特征应当被剔除，减少冗余）
  + 统计学建模基础：离散型随机变量相关度分析的一种思路是决策树模型和信息熵相关
  + 特征工程： [连续数值&离散类别处理方法](https://blog.csdn.net/cymy001/article/details/79154135)
2.encoder
  + 三种基于PCA的特征选择方式，结合[3D可视化](https://homepages.cwi.nl/~robertl/papers/2005/viip1/paper.pdf)
  + 基于SVM的[3D可视化方式](http://www-personal.umich.edu/~veeras/papers/4.pdf)

#### 应用

+ [基于知识图谱的小微企业贷款申请反欺诈](https://flashgene.com/archives/63679.html) 中国建设银行，201909
主要是（企业）节点、（干系人\亲属\担保）关系 表示和无关节点规约细节中有些不同。另外，试验部分要参考的一些点：
	
  + 图数据操作分析：neo4j + python igraph/networkX
  + 机器学习预排序算法：？_决策树系列的 xgboot，lightGBM 等_ 完全没有看懂过
  + 考虑数据特征的非独立同分布问题（节点标签信息可能影响其他节点） 
  
+ ...
  
### 毕业要求

CCF期刊[列表](http://history.ccf.org.cn/biaodan.jsp-contentId=2903028135856.htm)











  





