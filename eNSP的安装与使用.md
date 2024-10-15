# eNSP的安装与使用

### 企业网络仿真平台（华为模拟器）

### 路由、交换、无线、安全

### 

### 不同的命令在不同的模式下执行

#### <Huawei>用户视图

#### <Huawei>system-view

#### [Huawei]系统视图

#### [Huawei]int g0/0/0

#### [Huawei-GigabitEthernet0/0/0]接口视图

#### <Huawei>language-mode Chinese 修改语言环境为中文

#### ……其他试图



##### 注：只要命令具有唯一性，就可以缩写，也可以使用“Tab”键自动补全命令

##### “不知道”就按“？”键，显示帮助信息

##### 0/0/0 第几框/第几模块/第几接口



#### VRP命令行基础

#### VRP，通用路由平台（华为设备操作系统名称）

##### "."代表当前路径

##### “..”代表上一级目录

##### "/"代表根目录

#### 切换目录

##### <Huawei>cd  hcia/

#### 创建文件夹

##### <Huawei>mkdir  xxx

#### 删除文件夹

##### <Huawei>rmdir  xxx

#### 复制

##### <Huawei>copy  xxx  yyy

#### 移动

##### <Huawei>move  xxx  yyy

#### 删除

##### <Huawei>delete test

#### 恢复

##### <Huawei>undelete test

#### 永久删除

##### <Huawei>delete  /unreserved   test

#### 改名

##### <Huawei>rename xxx  yyy

#### 查看目录文件

##### <Huawei>dir

#### 查看文本内容

##### <Huawei>more  xxx

#### 显示当前工作路径

##### <Huawei>pwd

#### 查看设备的当前配置

##### <Huawei>display current-configuration

#### 保存配置

##### <Huawei>save

#### 修改设备名称

##### [Huawei]sysname

#### 查看设备已保存的配置

##### <Huawei>display saved-configuration

#### 恢复出厂设置（删除配置）

##### <Huawei>resst saved-configuration

#### 查看设备的启动参数

##### <Huawei>display startup

#### 修改设备的启动参数

##### <Huawei>startup ？

#### 对比配置文件差异

##### <Huawei>compare configuration

#### 关闭信息中心，防止命令输入被打断（默认启用，实际环境不要关）

##### [Huawei]undo info-center enable

#### 配置接口IP地址

##### [Huawei]int g0/0/0

##### [Huawei-GigabitEthernet0/0/0]ip address 

#### 测试网络连通性命令

##### <Huawei>ping 192.168.1.1



##### 