## KG

### 基础知识

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

#### 应用

+ [基于知识图谱的小微企业贷款申请反欺诈](https://flashgene.com/archives/63679.html) 中国建设银行，201909
主要是（企业）节点、（干系人\亲属\担保）关系 表示和无关节点规约细节中有些不同。另外，试验部分要参考的一些点：
	
  + 图数据操作分析：neo4j + python igraph/networkX
  + 机器学习预排序算法：？_决策树系列的 xgboot，lightGBM 等_ 完全没有看懂过
  + 考虑数据特征的非独立同分布问题（节点标签信息可能影响其他节点） 
  
+ ...
  
### 毕业要求

CCF期刊[列表](http://history.ccf.org.cn/biaodan.jsp-contentId=2903028135856.htm)











  





