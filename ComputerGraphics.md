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
   4. 虚火，成果，管理层效果评价和底层，元件，专业词汇字典，智慧之间的关系问题；准确性和深度

+ 图形学参考书 （photo）

+ e.g.问题分析 人脸美学评价方式：
  1. 几何特征网格模型
  2. 生物学特征从图像上的表述 纹理，五官轮廓
  3. 审美特征 艺术在 心理（相似性）、社会学（时代和人群）的描述

  + 原理（新特征的引入）创新 技术创新
  + 图形学因素：
   * 1. 人脸位置特征，光照
   * 2. 流体研究： 可能有大量公式

+ 图形学研究问题 CGraph 
  
  - 几何空间： 维度 位置 参数化
  - 节点，边，（曲）面，体
  - 视觉参数：反射率，折射率，亮度, 纹理，alpha值(alpha channel,不透明度)
  - 与图像（image）的转化: 直线段(图形，数学，连续) -投影、光栅（像素）化（离散化）+ 滤波 -> 帧frame（图像）-重建-> 图形。图像在像素（+深度）空间，图形在几何空间。pixels|vertices
  
  - 应用/优化/研究点：（硬件）和软件（大数据呈现），Accuracy -> Factually(传感，反光设备,对骨骼模型的重定向) -> Real time，变换transform/剪裁clipping/自由曲线交线intersaction/线和曲面遮挡culling，光照折射illumination使真实感可视化，云计算和网络传输，关注点预测，htweb红外室内定位5m*5m
  
  - 图形研究的四大问题
   + 1. 建模： 
       （1）设计模型表示方法(Model representation)场景，特征，物体建模；粒子系统和过程建模；建模为了更好地实现真实感或艺术性保障 ;坐标转换：model coordinates -(Model Transform)-> World Coordinates（右手坐标系） -(view transform)-> camera coordinates（左手坐标系，与世界坐标系为镜像关系。确定y轴和深度方向z轴（z-buffer,景深），观察点与两者呈现正交关系）
        (2)图形学中的建模方式:多边形(Polygonal)，渲染过程常常需要切分为三角形网格(triangle mesh)，保证一个三角形内部在同一个平面上。可以考虑均匀的（三角）网格模型或自适应的网格模型（减少损失）。辅以差值方法（tessellation）完成粗粒度的拟合(coarse piecewiee linear approximation实际上存在棱角)，C0连续（而不是流形：连续，内部不相交）;参数曲线和曲面;隐式曲面（内部有复杂的拓扑结构，为渲染需要重新做光照等，渲染效率低）;多分辨率的细分曲面；体结构的数据；基于语法(Grammar-based)和元模型(meta-model),譬如宜家的元件和组装家具过程；BSP树，将空间网格化，优化碰撞方式和效果渲染效率；粒子系统，流体表示，表征烟等粒子，该粒子系统有自身的运动模型
   + 2. 渲染： 视觉呈现。不同算法取决于真实感/艺术感/效率/_实时_/_直观_要求
     3. 动画： 表现变化的世界。算法： animation algorithm 物体形变 受（内/外）力 2D
     4. 交互： 与图形交互，就想在现实世界一样
     
  - 会议和期刊  
     1. [SIGGRAPH](http://kesen.realtimerendering.com/sig2019.html)
     2. SIGGRAPH Asia 
     
  - 核糖核苷酸
  
  - 15fps(支持实时显示) 30 72fps（in-detectable）显示 帧率 对硬件(Graphics Process Unit)的要求：200亿 元器件，速度(写死的单元)和灵活性（可编程）的折中。由大数据小指令集的特性，GPU能支持通用计算，如科学计算
  
  - 图形显示(Display) ：参考一个pipline（图）
   + 1.视口（viewport）!= 窗口(window);
   + 2.3D三维坐标系中的点经过投影（在每个轴向上的切片）到二维坐标系，然后光栅化（包括_高维形体_显示，都需要投影到二维坐标系）；
   + 3.显示设备：仍然是隔行扫描或逐行扫描；
   + 4.帧缓存(frame buffer): （1）color buffer:RGB颜色空间(2^24)+2^8 alpha值 = 真彩色，(2)alpha buffer: alpha channel使能支持场景叠加(3) z-buffer (4)stencil buffer模板缓冲 (5) frame buffer (6)accumulation buffer :柔化边界，软阴影;
   + 5:折屏，曲面屏拼接变形显示 结构光；学生创新中心 cave（-4） 系统，投影设备 + 人定位；头盔显示：计算模块和轻便性难以平衡，但是沉浸感好，在5G驱动中有无线的可能性；3D显示：perspeca高速旋转，在每个位置展示截面的曲面屏,depthCube半透明膜叠加
   + 6.光照和阴影；
   + 7.投影（矩阵变换的一种）。投影和模拟：平行投影（CAD常用），直角投影，透视投影等，有成熟的技术
   + 8.剪裁（clipping）：矩形，多边形非规则，弧形，有成熟的硬件产品和技术;8.图元primitive|fragment.


  
+ 研究开展：老师 前辈 沟通交流能力

### 论文阅读和选题

1.1. 知识图谱生成[过程可视化](https://medium.com/@sderymail/challenges-of-knowledge-graph-part-1-d9ffe9e35214)

1.2. [供应链](https://pdfs.semanticscholar.org/c96d/3bc5fa74dc01acc70a6212a583f909435cca.pdf) intergrated sc 中的可关注结构：
  + 产品状态变化： material -> intermeidate -> finished 
  + 供应链层级化的站点：sites organized in different levels 
  + 需要量化的特征 :
    * 1. 需求（数量volumn、组合mix）; 过程（生产yield、停机时间machine downtime、运输可靠性transportation reliabilities）; 供应（零件质量part quality, 交付可靠性delivery reliabilities）
	  
    *  库存 inventory 选址和容量变化范围（柔性）
    *  或 物流 material flow 结构 组织结构organization structure 障碍点barrier
	+ 信息流动 information flow 透明性是不可保证的，因此集中控制原材料 物流不可取 。分布式控制：在每个单元根据本地信息决策
	+ 网络参与者 participants of network[BIS19](https://link.springer.com/chapter/10.1007/978-3-030-20482-2_16#Sec5):suppliers, manufacturers, logistics providers, wholesalers批发商, distributors and retailers
	+ 
1.3 水力学模型和仿真计算 [google洪水预测模型]
2.1. [链式反应装置](http://geometry.cs.ucl.ac.uk/projects/2019/causal-graphs/)
  + 因果图(Casual Grpah)支持链式反应装置(Chain reaction contraptions)
 
2.2. [基于谱的动态图变化检测](http://www.lix.polytechnique.fr/~maks/papers/SpectralMeasures.pdf) spectral method: 谱图理论。动态网络（时间+网络结构）：噪声中边协作进化，网络结构改变。拉普拉斯矩阵。
  1. 动态图变化捕捉：
    + animation - time to time mapping
    + timeline - time to space mapping[4]
  2. 绘制技术[6,7,11,13,15,26,25]完成图探索(graph exploring)[3] update layout while preserving the mental map
    + 基于顶点的减少节点位移
      * 15: force-directed layout + 节点寿命vertex age 
      * 13: force-directed layout力导向布局 + 节点固定权重node pinning weights 
    + 基于光谱法减少节点位移
      * 6：经典谱布局 -> 适应动态图
      * 10,26,27: 布局后处理
    + 畸变区/失真区检测 distortion
      * 大型网络可视化中检测时间窗口和相关区域[16][17]
    + 结合distorted area 和 force layout
  3.谱分析
    + 0. 谱：将信号（视频/音频/图像/图）分解为简单元素(小波基/图基)的线性组合。其中，分解元素常是线性无关(正交)的。
    + 1.图的拉普拉斯矩阵(D-W)
    + 2.对该矩阵的因子分解是一种谱聚类的方式
    + 3.三种基于PCA的[3D可视化方式](https://homepages.cwi.nl/~robertl/papers/2005/viip1/paper.pdf)

    
2.3. [图语义标注](http://www.cs.cityu.edu.hk/~rynson/projects/layout/GraphicsLayout.html)完成content-aware
