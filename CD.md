### 社群发现
+ 基本算法


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
      
+ 多标签分类问题[MLC](https://zhuanlan.zhihu.com/p/58076177)
  1. 转换类方法
    * 枚举所有多标签组合 -> 转化为单标签分类
    * 转化为二分类chain（CC, read et al,2011）,每一个未分类问题依赖上一个二分类问题结果，复杂度高
  2.算法适应类
    * 基于multi-label entropy的决策树
    * 最大化margin 核
    * label相关性约束 考虑转移触发条件、触发概率的[条件随机场](https://zhuanlan.zhihu.com/p/34261803) 最大熵 [CIKM'05](https://people.cs.umass.edu/~mccallum/papers/condmultilabel-cikm05.pdf)

  3. 集成类
  4. 神经网络类
      
+ [neo4j官网LPA举例] 药品副作用标签传播
  + DDI 药品相互作用
  + 数据集：
    + 569药品
    + LPA输入数据：维度建模：副作用4192-D (binary,每个维度代表一种副作用是1/否0存在)，未记录的副作用10093-D，化学分子式881-D(每个维度代表子结构是1/否0)
    + CS(Chemical Similarity),LSES(Labeled side effect similarity),OSES(Off-labeled side effect similarity)三个矩阵，分别由 TC(Jaccard Index) 计算出drugi drugj副作用张量、未记录副作用张量、分子式张量的相似度得到
    + 网络节点为D,邻接矩阵A为三个相似度度量矩阵之积，aij值为Weighted_E权重，当前节点CD,已知与CD存在DDI的节点标记为阳性(positive)
      + LPA细节：标签传播过程
    + LPA输出：52416成对的DDI
    
 + 特征处理和提取方法[哈工2016硕士学位]](http://oss.wanfangdata.com.cn/www/download.ashx/%E6%90%9C%E7%B4%A2%E5%B9%BF%E5%91%8A%E7%82%B9%E5%87%BB%E7%8E%87%E9%A2%84%E6%B5%8B%E4%B8%AD%E7%9A%84%E5%86%B7%E5%90%AF%E5%8A%A8%E9%97%AE%E9%A2%98%E7%A0%94%E7%A9%B6.ashx?isread=true&type=degree&resourceId=D01098733&transaction=%7B%22id%22%3Anull%2C%22transferOutAccountsStatus%22%3Anull%2C%22transaction%22%3A%7B%22id%22%3A%221175598908273876992%22%2C%22status%22%3A1%2C%22createDateTime%22%3Anull%2C%22payDateTime%22%3A1569119595961%2C%22authToken%22%3A%22TGT-8522957-ULzXlATKyjYy1NntKayzY9VbZVBB6Hg2FyfdTHJBylqNcfTudV-my.wanfangdata.com.cn%22%2C%22user%22%3A%7B%22accountType%22%3A%22Group%22%2C%22key%22%3A%22shjtdxip%22%7D%2C%22transferIn%22%3A%7B%22accountType%22%3A%22Income%22%2C%22key%22%3A%22ThesisFulltext%22%7D%2C%22transferOut%22%3A%7B%22GTimeLimit.shjtdxip%22%3A30.0%7D%2C%22turnover%22%3A30.0%2C%22orderTurnover%22%3A0.0%2C%22productDetail%22%3A%22degree_D01098733%22%2C%22productTitle%22%3Anull%2C%22userIP%22%3A%22202.120.11.13%22%2C%22organName%22%3Anull%2C%22memo%22%3Anull%2C%22orderUser%22%3A%22shjtdxip%22%2C%22orderChannel%22%3A%22pc%22%2C%22payTag%22%3A%22%22%2C%22webTransactionRequest%22%3Anull%2C%22signature%22%3A%22ZmVInQo1bjMugcfRu6utDBypUI9RmlyupuCMC4ZJVwJsIS4bKmsQO6vzMvN79HYEKsLEpVZQ%2FKsW%5Cnmb1i%2F2fWujfZCkzsPBxEQXJIKaZ6n4chOklSSuk%2BFgISK3VAHeEoakRyeUAieTyxzkaZj8mbUHs1%5Cn7Dd5ZhF8KJJH9W%2Feoss%3D%22%2C%22delete%22%3Afalse%7D%2C%22isCache%22%3Afalse%7D)
  1. 连续性特征，离散型特征（独特编码）
  2. 线性函数归一化、零均值归一化
  3. 特征选择结果评价指标：AUC

+ 带有缺失数据的推荐系统冷启动 -- N维马尔可夫随机场作为先验约束的矩阵分解模型[南邮2016博士学位]（http://oss.wanfangdata.com.cn/www/download.ashx/%E5%9F%BA%E4%BA%8E%E5%B1%9E%E6%80%A7%E7%9A%84%E5%86%B7%E5%90%AF%E5%8A%A8%E6%8E%A8%E8%8D%90%E9%97%AE%E9%A2%98%E7%A0%94%E7%A9%B6.ashx?isread=true&type=degree&resourceId=Y3378438&transaction=%7B%22id%22%3Anull%2C%22transferOutAccountsStatus%22%3Anull%2C%22transaction%22%3A%7B%22id%22%3A%221175606353935212544%22%2C%22status%22%3A1%2C%22createDateTime%22%3Anull%2C%22payDateTime%22%3A1569121371145%2C%22authToken%22%3A%22TGT-8364687-9xMJyeqDsgArjmyGRykMbpDrRYGbHOevksfWDduvViO2fLqIfT-my.wanfangdata.com.cn%22%2C%22user%22%3A%7B%22accountType%22%3A%22Group%22%2C%22key%22%3A%22shjtdxip%22%7D%2C%22transferIn%22%3A%7B%22accountType%22%3A%22Income%22%2C%22key%22%3A%22ThesisFulltext%22%7D%2C%22transferOut%22%3A%7B%22GTimeLimit.shjtdxip%22%3A30.0%7D%2C%22turnover%22%3A30.0%2C%22orderTurnover%22%3A0.0%2C%22productDetail%22%3A%22degree_Y3378438%22%2C%22productTitle%22%3Anull%2C%22userIP%22%3A%22202.120.11.13%22%2C%22organName%22%3Anull%2C%22memo%22%3Anull%2C%22orderUser%22%3A%22shjtdxip%22%2C%22orderChannel%22%3A%22pc%22%2C%22payTag%22%3A%22%22%2C%22webTransactionRequest%22%3Anull%2C%22signature%22%3A%22ZXvhae4WqnHNA6JDxdkNPpJozjiWHWF7QpqMft4fmKEPx5G24cId%2F99y0O7l3GiIrge3yyuQ6zjY%5Cn1rActoi3W%2Fd986loJ%2Fig%2BpGbx4GiqyfNFhKAgiBn9UWiJqUGYEom3VO3ayii6TsYB%2B7ezl93%2FlNq%5Cn%2BA9P7IFZJjuHhqunVSY%3D%22%2C%22delete%22%3Afalse%7D%2C%22isCache%22%3Afalse%7D）

  1. 基于属性的冷启动：
     新用户和新项目没有历史交互信息 -- 用马尔可夫场做先验约束的矩阵分解模型（MRF-MF）,再使用轮换最小二乘法(ALS-like)求解

  2. N维马尔科夫随机场(MRF)站点集合：对站点（像素-R2、用户-Rn）,邻居为4/8个像素、2^n个点，维数灾难-->改变近邻系统1使用r半径近邻的处理方式，当拥有某个属性的用户超过一定数量之后，系统不再将不同属性的用户当做近邻。根据马尔可夫性，非临近用户的特征不会对当前用户隐特征产生影响，因此能将属性不同的用户从依赖用户中排除。

规则模型 --》 概率模型
    
