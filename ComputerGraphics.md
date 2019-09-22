## 图形学

### 课堂笔记

+ 数字艺术实验室研究方向：
  - rendering 图像 Image
  - interaction 交互 （本科课程）
  - computer graphics 图形
  - animation(数媒实验室的研究方向)

  - 比较：
    * CAD 关注建模
  	* 图像 研究分区和分类问题-》转化为图形-》转化为图像完成渲染

+ 研究过程
  1. 问题发现（质疑）--> 人脸美学评价方式
    * 质疑什么：前文论述掩盖的研究缺陷，社会的发展前进空间。任何成果都有问题。

  2. 分析过程（注意问题描述和问题域的确定）
      + 细化目标：回归问题 or 分类聚类问题 or 前人对问题的研究 ，完成问题的补充描述
      + 问题边界：对输入数据（类别）的确定，明确问题域
      + 关联因素：特征的选择和主成分分析（key point）
      + 方法：和前人方法的对比：问题域的区别，特征值的区别，或是纯技术层面的效率改进。在这一步需要理解现有技术。

        * 理论分析
        * 实验比较：新方法带来了进步
        * 应用场景：模糊/口号 -> 具体
        * 逻辑漏洞：理工科应当避免：逻辑矛盾，数据真实性（量级，单位）

  3. 细节
      * 先分析相关问题 及子问题 ，再考虑方法

      * 先画算法和问题解决分析的流程图，再细化到某一个细节的ML学习方法或特征点选择的方法

      * 先选择算法流程图/数学方法描述,再选择文字/代码(可能有歧义)

      * 研究笔记整理：参考文献按照引用方式整理，方便找思路和整合，最优化构架知识结构

 + xsjiu99@cs.sjtu.edu.cn 方法论
   1. 最优化知识结构
   2. 能量最小化
   3. 编程思维，？图学思维

+ 图形学参考书 （photo）

+ e.g.问题分析 人脸美学评价方式：
  1. 几何特征网格模型
  2. 生物学特征从图像上的表述 纹理，五官轮廓
  3. 审美特征 艺术在 心理（相似性）、社会学（时代和人群）的描述

  + 原理（新特征的引入）创新 技术创新
  + 图形学因素：
    1. 人脸位置特征，光照
    2. 流体研究： 可能有大量公式

+ 图形学研究问题 CGraph 
  
  - 几何空间： 维度 位置 参数化
  - 节点，边，（曲）面，体
  - 视觉参数：反射率，折射率，亮度
  - 与图像（image）的转化: 直线段(图形，数学，连续) -光栅化（离散化）-> 帧frame（图像）--> 图形
  - 应用/优化/研究点：（硬件）和软件（大数据呈现），Accuracy -> Factually(传感，反光设备,对骨骼模型的重定向) -> Real time，变换transform/剪裁clipping/自由曲线交线intersaction/线和曲面遮挡culling，光照折射illumination使真实感可视化，云计算和网络传输，关注点预测，htweb红外室内定位5m*5m
  - 建模： 场景，特征，物体建模；粒子系统和过程建模；
  - 算法： animation algorithm 物体形变 受（内/外）力 2D
  - 核糖核苷酸
  - 15 30 72 fps 帧率 对硬件的要求：200亿 元器件
  
+ 研究开展：老师 前辈 沟通交流能力

### 论文阅读和选题

1. 知识图谱生成[过程可视化](https://medium.com/@sderymail/challenges-of-knowledge-graph-part-1-d9ffe9e35214)
2. [动态网络可视化](http://www.lix.polytechnique.fr/~maks/papers/SpectralMeasures.pdf)
  + spectral method: 谱图理论
  + 动态网络（时间+网络结构）：噪声中边协作进化，网络结构改变。拉普拉斯矩阵
  
3. [供应链](https://pdfs.semanticscholar.org/c96d/3bc5fa74dc01acc70a6212a583f909435cca.pdf) intergrated sc 中的可关注结构：
	+ 产品状态变化： material -> intermeidate -> finished 
	+ 供应链层级化的站点：sites organized in different levels 
	+ 需要量化的特征 :
	  1. 需求（数量volumn、组合mix）; 过程（生产yield、停机时间machine downtime、运输可靠性transportation reliabilities）; 供应（零件质量part quality, 交付可靠性delivery reliabilities）
	  
	+ 输出  库存 inventory 选址和容量变化范围（柔性）
	+ 或 物流 material flow 结构 组织结构organization structure 障碍点barrier
	+ 信息流动 information flow 透明性是不可保证的，因此集中控制原材料 物流不可取 。分布式控制：在每个单元根据本地信息决策
	+ 网络参与者 participants of network[BIS19](https://link.springer.com/chapter/10.1007/978-3-030-20482-2_16#Sec5):suppliers, manufacturers, logistics providers, wholesalers批发商, distributors and retailers
	+ 
