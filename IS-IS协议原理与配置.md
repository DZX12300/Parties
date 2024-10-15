# IS-IS协议原理与配置



[TOC]

### 应用场景：

#### 园区网：区域多样、策略多变、调度精细（相当于城市交通，复杂）

![image-20240928093019869](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928093019869.png)



#### 骨干网：区域扁平、收敛极快、承载庞大（相当于高速，简单）

![image-20240928093101097](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928093101097.png)





## 一、IS-IS协议基本原理

![image-20240928093838424](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928093838424.png)

#### 集成IS-IS特点

1. ##### 支持CLNP网络、IP网络

2. ##### 工作在数据链路层

#### OSPF特点

1. ##### 目前支持IP网络

2. ##### 工作在IP层



## 二、路由计算过程

![image-20240928094112269](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928094112269.png)



## 三、地址结构

![image-20240928094208846](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928094208846.png)



## 四、路由器分类

### IS-IS路由器的三种类型

- ##### Level-1路由器(只能创建level-1的LSDB)

- ##### Level-2路由器(只能创建level-2的LSDB)

- ##### Level-1-2路由器(路由器默认的类型，能同时创建level-1和level-2的LSDB)

![image-20240928095839829](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928095839829.png)

##### 总结：L1路由器只能和本区域的L1路由器建立邻接关系

##### 			L2路由器既可以和本区域的L2路由器建立邻接关系，也可以和不同区域的L2路由器建立邻接关系

##### 			L1只能和L1建立邻接，L2只能和L2建立邻接



## 五、邻居hello报文

![image-20240928100413901](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928100413901.png)

##### IS-IS目前只支持点对点的广播网络类型



## 六、邻居关系建立

![image-20240928104742915](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928104742915.png)

##### ISO10589使用两次握手，RFC3373定义了P2P三次握手机制

![image-20240928105057521](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928105057521.png)

##### MA网络类型的邻居关系建立必须是三次握手



## 七、DIS及DIS与DR的类别

![image-20240928105032019](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928105032019.png)

|    类比点    |             ISIS-DIS             |       OSPF-DR       |
| :----------: | :------------------------------: | :-----------------: |
|  选举优先级  |       所有优先级都参与选举       |  0优先级不参与选举  |
| 选举等待时间 |         2个hello报文间隔         |         40s         |
|     备份     |                无                |      有（BDR）      |
|   邻接关系   |    所有路由器相互都是邻接关系    |  DR之间是2-way关系  |
|    抢占性    |              会抢占              |      不会抢占       |
|     作用     | 周期发送CSNP，保障MA网络LSDB同步 | 主要为了减少LSA泛洪 |

##### 注意：术语对照表

![image-20240928110409916](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928110409916.png)



## 八、链路状态信息

### 载体

#### LSP PDU--用于交换链路状态信息。

- ##### 实节点LSP

- ##### 伪节点LSP(只在广播链路存在)

#### SNP PDU-用于维护LSDB 的完整与同步，且为摘要信息。

- ##### CSNP(用于同步LSP)

- ##### PSNP(用于请求和确认LSP)

#### 协议报文都分为Leve1-1和Level-2两种，在MA网络中所有协议报文的目的MAC都是组地址:

- ##### Level-1地址为:0180-C200-0014

- ##### Level-2地址为:0180-C200-0015

### 交互

![image-20240928110912370](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928110912370.png)



## 九、路由算法

![image-20240928112121552](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928112121552.png)



## 十、网络分层路由域

![image-20240928112738359](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928112738359.png)

##### 总结：L2路由器所在的范围称之为骨干 

##### 			L1/2路由器“区域边界”

##### 			L1路由器只能和本区域的L1路由器建立邻接关系

##### 			L2路由器既可以和本区域的L2路由器建立邻接关系，也可以和不同区域的L2路由器建立邻接关系

##### 			L1路由器只拥有本区域的路由

##### 			L1路由器的区域相当于OSPF当中的“完全末梢”

​			

## 十一、区域间路由

![image-20240928114428167](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240928114428167.png)



## 十二、IS-IS与OSPF差异性

|    差异性    | IS-IS | OSPF |
| :----------: | :---: | :--: |
|   网络类型   |  少   |  多  |
|   开销方式   | 复杂  | 简便 |
|   区域类型   |  少   |  多  |
| 路由报文类型 | 简单  | 多样 |
|     路由     |       |      |
|              |       |      |
|              |       |      |

![image-20241008104741483](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20241008104741483.png)

l
