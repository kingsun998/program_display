
### 展示作品
包含两个项目


#### 基于CAN通信的温度传感器测试标定软件
**内容**：针对不同传感器开发测试软件。具备将测试数据进行 可视化，协议解析，传输，文件存储，数据交互，数据刷写等功能。

**开发技术**：c++ QT Mqtt

**软件介绍**：
* 测试软件具备CAN报文接收，发送，解析，保存功能，存储形式为EXCELL表；
* 软件可实现EGTS 广播报文到温度的解析以及FMI的解析，数据具有图像化显示功能，坐标轴可调节。温度数据以及故障解析以EXCALL表形式长时间保存；
* 软件集成有CAN bootloader刷写功能，将二进制文件刷写至硬件；
* 软件具有多通道和单通道绝缘电阻仪数据获取功能。
* 软件具有与生产MES系统进行数据交互的功能，采用MQTT协议，报文订阅的方式发送。

**负责工作**：软件编写，调试与部署。

**团队职责**: 理解产品需求，完成代码的编写。在生产环境中完成测试与部署。

**最困难的问题**: 在程序运行过程中产生空指针异常。

**采取措施与解决方法**：

解决步骤：
1. 首先对异常代码进行定位和排查，发现在多线程数据保存时偶尔会出现空指针异常。
2. 对代码进行局部修改，增加判断以避免空指针，但是造成了堵塞。
3. 随后更换第三方库，仍会出现此问题。
4. 对保存业务代码进行整体重构。使用 Reactor+任务队列 的模式解决此问题。

**截图**：
![截图1](https://github.com/kingsun998/program_display/blob/master/images/1_1.PNG)
![截图2](https://github.com/kingsun998/program_display/blob/master/images/1_2.PNG)
![截图3](https://github.com/kingsun998/program_display/blob/master/images/1_3.PNG)
![截图4](https://github.com/kingsun998/program_display/blob/master/images/1_4.PNG)

#### Linux文件服务器
**内容**：基于Linux开发的文件服务器和客户端，同时附加密钥服务器，以非对称加密进行密钥协商，对称加密进行数据传输，同时也提供文件校验功能。

**开发技术**：c++ libevenet openssl linux通信 共享内存 QT

**软件介绍**：

* 基于LInux开发文件服务器，实现安全文件文件传输。
* 使用 Reactor架构，构建服务器。
* 提供秘钥协商服务，采用RSA协商算法，采取非对称加密算法进行秘钥协商和用户认证；
* 使用共享内存的方式进行进程间通信
* 提供通信加密服务，采用DES对称加密算法传输通信信息
* 提供多线程文件下载，构建线程池。
* 提供文件校验服务，计算文件哈希值，保证文件的正确性。



**最困难的问题**: epoll线程池任务分配，共享内存操作

**采取措施与解决方法**： 在程序运行时出现任务重复执行的问题，经排查发现是任务分配的问题。当读事件已分配但还未处理，循环重新将其分配给另一线程，导致多重分配。

解决方法：
通过查询，将epoll的监听和通信事件均置于边缘触发模式，解决此问题。



**截图**：

![截图1](https://github.com/kingsun998/program_display/blob/master/images/2_1.png)
![截图2](https://github.com/kingsun998/program_display/blob/master/images/2_2.png)
![截图3](https://github.com/kingsun998/program_display/blob/master/images/2_3.png)
![截图4](https://github.com/kingsun998/program_display/blob/master/images/2_4.png)
