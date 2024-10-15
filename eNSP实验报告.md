# AAA(认证、授权、计费)



# FTP服务配置

##### 文件传输协议

##### 使用c/s架构

##### 基于传输层封装TCP20、21端口

##### [Huawei]dis tcp status 

##### 20端口为数据连接（传输用户数据）

##### 21端口为控制连接（传输协议数据）

![命令1](C:\Users\16042\Desktop\ensp\命令1.png)

##### 文件的上传下载会引用当前设备的当前路径（使用pwd命令查看）

##### 用户密码与数据截获





# 密码设置技巧

##### notepad记事本

##### calc计算器

##### charmap字符映射表



# 设备管理（Telnet、SSH、HTTP、SNMP）

#### 本地、远程

#### 命令、图形

#### 带内、带外

##### 带内：管理和业务流量混在一起的（一条线路）

##### 带外：管理和业务流量分离（两条线路）

#### 流量：管理流量，业务流量

##### 管理流量：

##### 业务流量：

# Console控制台本地管理配置

#### [Huawei]user-interface console 0

#### [Huawei-ui-console0]authentication-mode password

#### [Huawei-ui-console0]set authentication password cipher 123456

#### [Huawei-ui-console0]idle-timeout 0 30

#### 或者

#### [Huawei]user-interface console 0

#### [Huawei-ui-console0]authentication-mode aaa

#### [Huawei-ui-console0]aaa

#### [Huawei-aaa]local-user hcie password cipher huawei

#### [Huawei-aaa]local-user hcie service-type terminal

#### [Huawei-aaa]local-user hcie …..?

#### 注：[Huawei-ui-console0]idle-timeout 0 0	永不超时



# 命令权限级别（0-15）

#### 0	访问

#### 1	监控

#### 2	配置

#### 3	管理

![image-20240910105239719](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240910105239719.png)

### Telnet 配置1

#### [Huawei]telnet serverenable(eNsp 中默认启用，真实设备默认一般都是禁用的)

#### [Huawei]user-interface vty 0 4

#### [Huawei-ui-vty0-4]authentication-mode password

#### [Huawei-ui-vty0-4]set authentication password cipher 12345

#### [Huawei-ui-vty0-4]user privilege level 3

#### <Client>telnet 192.168.5.2



### Telnet 配置2

#### [Huawei]telnet server enable

#### [Huawei-ui-vty0-4]authentication-mode aaa

#### [Huawei]aaa

#### [Huawei-aaa]local-user hcia password cipher 123456

#### [Huawei-aaa]local-user hcia service-type telnet

#### [Huawei-aaa]local-user hcia privilege level 3

#### [Huawei-aaa]local-user hcia access-limit 1

#### [Huawei-aaa]local-user hcia ……?





![image-20240910142007492](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240910142007492.png)

##### 第一步：rsa	创建密钥对

##### rsa	非对称加密算法

##### inbound	入方向

##### ssh协议

##### ssh user huawei authentication-type password

##### stelnet server enable 启用ssh服务

##### ssh client first-time enablestelnet 192.168.1.2(在系统视图配)





##### Windows环境下添加硬件，执行命令 hdwwiz，添加一张网卡。(可选操作，非必须)

##### 配置 AC的 Web访问(eNSP……100 版本)

##### <AC6605>dis tcp status

##### <AC6605>display vlan brief

##### [AC6605-Vlanif1]ip address 192.168.234.111 24（与cloud在一个网段）

##### [AC6605-Vlanif1]ping 192.168.234.1

##### 客户端使用浏览器打开

##### https://192.168.234.111

##### 用户名:admin	密码:admin@huawei.com



# 端口隔离

##### 端口隔离作用于启用了隔离功能的端口之间

##### interface GigabitEthernet0/0/1

#####   port-isolate enable group 1

##### interface GigabitEthernet0/0/2

#####   port-isolate enable group 1

##### interface GigabitEthernet0/0/3

#####   port-isolate enable group 2

##### interface GigabitEthernet0/0/4

#####   port-isolate enable group 2

##### 组内不能通信，组间可以通信





# 端口安全

#### 设备已重启，MAC地址会消失第一种(动态地址不保存)只固定数量

#### [Huawei-GigabitEthernet0/0/4]port-security enable

#### [Huawei-GigabitEthernet0/0/4]port-security max-mac-num2(最大数量）

#### 

#### 第二种(静态地址保存)固定地址

#### [Huawei-GigabitEthernet0/0/4]port-security enable(给数量)

#### [Huawei-GigabitEthernet0/0/4]port-security max-mac-num 2

#### [Huawei-GigabitEthernet0/0/4]port-security mac-address sticky

#### [Huawei-GigabitEthernet0/0/4]port-security mac-address sticky MAC地址 vlan 1



# 镜像技术

#### 基于端口	(没有针对性)

基于流		(有针对性)
1 观察端口、2 锁定流量、3 流量分类、4 流量行为、5 流量策略、6 接口引用

#### LLDP，链路层发现协议(拓扑发现)

### 基于端口

#### observe-port interface g0/0/0 （选择观察端口）

#### interface g0/0/1

#### mirror to observe-port inbound（入方向）

#### 或者

#### interface g0/0/2

#### mirror to observe-port inbound

![img](https://cdn.nlark.com/yuque/0/2024/png/42412163/1726021179925-09125e2e-ff8b-44d1-b9c8-61f15faa7227.png)





### 基于流

![img](https://cdn.nlark.com/yuque/0/2024/png/42412163/1726022979240-1270425b-24f7-4943-b075-f9fc82efe15f.png)

#### observe-port interface Ethernet2/0/1

#### acl  number 2000

#### rule 5 permit source 192.168.1.10  0（0.0.0.0  对应固定 可以缩写 锁定地址）

#### 1.traffic classifier c1 operator or （默认一个条件）

#### if-match acl 2000

#### 2.traffic behavior b1 

#### mirror to observe-port（将1和2绑一起）

#### traffic policy p1

#### classifier c1 behavior b1

#### interface Ethernet2/0/0  （被监控端口）

#### traffic-policy p1 inbound









![img](https://cdn.nlark.com/yuque/0/2024/jpeg/42412163/1726022003231-9c918919-41e3-4fdf-a233-e9360e63327f.jpeg)

### LLDP，链路层发现协议（拓扑发现)

#### [r1]lldp enable

#### [r1]lldp ..?

#### [r1-GigabitEthernet0/0/1]lldp enable

#### [r1-GigabitEthernet0/0/1]lldp .....?

#### <r1>display lldp local（本地信息）

#### <r1>display lldp statistics（统计信息）

#### <r1>display lldp neighbor（邻居）

#### <r1>display lldp neighbor brief（精简信息）

![image-20240911141301108](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240911141301108.png)

### 静态路由

#### 路由?源节点到目标节点进行路径选择的过程

#### 路由器?在此过程中负责路径判断的网络设备

#### 路由技术?如何确定一条最佳路径的方法

#### 路由表“地图”1 我在哪儿(源);2我要去哪儿(目标);3怎么去(最佳路径)

##### 	直连，配置IP地址，接口 UP，自动进入路由表

##### 	非直连，需要配置静态或动态路由

#### 下一跳(以太网)

##### 	1 数据下一次所提交的地方

##### 	2 对端设备接口 IP 地址

#### 出接口，数据从自己的哪个接口转发出去（应用于点到点链路）

### 全网互通

##### 	1.所有路由器的路由表都应该要拥有所有网段条目

##### 如果某个路由器的路由表篇缺少某个条目......不可达！

##### 	2.路由表状态一致的过程

##### 路由器IP地址配置（不同接口，不同网段；相同链路，相同网段）

##### [Huawei]ip route-static 192.168.2.0 24 192.168.1.2(下一跳)

##### [Huawei]ip route-static 192.168.2.0 24 G0/0/14出接口)

##### <Huawei>display ip routing-table验证

##### ping 192.168.4.2

##### tracert 192.168.4.2

##### 静态路由协议特点:

##### 1 人为配置，手工添加

![image-20240911154851345](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240911154851345.png)

### 静态路由协议特点:

##### 1 人为配置，手工添加

##### 2 不能根据拓扑结构的变化而自动变化

##### 3 适用于小型网络

##### 4 中大型网络中针对性的结合使用

##### 5 精确控制数据流向



### 提醒：静态路由缺什么配什么，动态路由有什么配什么



### 路由优先级

#### 数值越低越优先

#### 取值范围0~255

#### 直连	0

#### 静态	60

#### RIP	100

#### OPSF	10	150

#### ISIS	15

#### BGP	255



### 动态路由协议配置

##### RIP、OSPF、ISIS（骨干网络）、BGP

##### 每个路由器只需完成白身初始化配置即可(无需关心目标网络和下一跳)



##### RIP 配置

##### [zdx-R1]rip

##### [zdx-R1-rip-1]network 192.168.1.0

##### [zdx-R1-rip-1]preference 50



##### OSPF 配置 1(精确宣告)

##### [zdx-R1]ospf

##### [zdx-R1-ospf-1]area 0（单区域划分为0）

##### [zdx-R1-ospf-1-area-0.0.0.0]network 192.168.1.0 0.0.0.255

##### OSPF 配置 2(模糊宣告)

##### [zdx-R1]ospf

##### [zdx-R1-ospf-1]area 0（单区域划分为0）

##### [zdx-R1-ospf-1-area-0.0.0.0]network 0.0.0.0 0.0.0.0



### 路径跟踪

##### netstat -an(windows 环境下查看网络活动连接状态

##### tracert www.baidu.com跟踪目标主机，查询数据转发路径)

##### ping www.baidu.com(查询目标主机的 TTL值，判断操作系统类型)



### TTL

##### 1 生存时间 或 时间周期

##### 2 IP 数据包中的:值(三层）

##### 3 取值范围 0-255(1个字节）

##### 4 不同节点，其默认值不同 32、64、128、255

##### 5 可以通过 ping 127.0.0.1，了解自身节点的默认 TTL 值

##### 6 TTL值可修改

##### 7 某些技术也会影响 TTL值发生变化

##### 8 经过一个路由器，数值减1

##### 9 当数值为0的时候，数据丢弃

##### 10 防止数据无限循环(消除环路)



### DHCP动态主机配置协议实现网络参数的自初分配(IP 地址、掩码、网关、DNS...)

#### 手动配置 IP 地址:

##### 1 不方便，工作量大

##### 2 不便于管理

##### 3 容易出错

##### 4 地址冲突

##### 5 地址利用率不高

##### 6 没有统一的规划

#### DHCP 工作原理

##### 1 发现

##### 2 回应

##### 3 请求

##### 4 确认



### DHCP 租约时间

##### 默认一天（不同平台、不同厂商、不同设备存在差异）

##### 50% 		第一次续约请求

##### 87.5% 	第二次续约请求

##### 接口地址池配置(只为一个网段分配网络参数)

##### 自动引用接口地址的网络参数给客户端

![image-20240912145417320](C:\Users\16042\AppData\Roaming\Typora\typora-user-images\image-20240912145417320.png)



##### [Huawei]dhcp enable

##### [Huawei-GigabitEthernet0/0/0]ip add 192.168.1.1 24

##### [Huawei-GigabitEthernet0/0/0]dhcp select interface

##### [Huawei-GigabitEthernet0/0/0]dhcp server dns-list 8.8.8.8

##### [Huawei-GigabitEthernet0/0/0]dhcp server......？



#### 验证

##### PC>ipconfig(查看网络参数)

##### PC>ipconfig/release(释放IP 地址)

##### PC>ipconfig/renew(重新请求)

##### <Huawei>display ip pool name net1

##### <Huawei>display ip pool ...?



#### 全局地址池配置(为所有网段分配网络参数)

##### [Huawei]dhcp enable

##### [Huawei]ip pool net1

##### [Huawei-ip-pool-net1]network 192.168.1 .0 mask 24

##### [Huawei-ip-pool-net1]gateway-ist 192.168.1.1（网关）

##### [Huawei-ip-pool-net1]dns list 12.12.21.12（DNS服务器）

##### [Huawei-ip-pool-net1]static-bind ipaddress 192.168.1.250 mac-address 5489-9872-202f（静态绑定MAC地址）

##### [Huawei-ip-pool-net1]excluded-ip-address 192.168.1.254（排除什么地址不分配）

##### [Huawei-ip-pool-net1]lease day 2 hour 3 minute 4（租约时间）

##### [Huawei-ip-pool-net1]....?

##### [Huawei-GigabitEthernet0 /0/0]dhcp select global



#### DHCP大部分都是广播数据包，而广播数据包只能在同一网段内传输



#### DHCP中继配置(跨网段场景，在客户端所在的网关接口上配置)

##### [Huawei]dhcp enable

##### [Huawei-GigabitEthernet0/0/0]dhcp select relay（选择此接口作为DHCP的中继）

##### [Huawei-GigabitEthernet0/0/0]dhcp relay server-ip 192.168.1.1



