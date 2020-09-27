---
layout:post
---


## 方案

### 策略

1. 五支箭并发

    1. R1流程

       | 所需时间 | 时间点 | 备注                   | 机构动作 |
       | -------- | ------ | ---------------------- | -------- |
       | 0s       | 0s     | 准备开始               | 准备射箭 |
       | 0.3s     | 0.3s   | 开始射箭               | 开始射箭 |
       | 0.5s     | 0.8s   | 箭矢发射完毕           | 箭矢发射 |
       | 2s       | 2.8s   | 移动到箭架处           | 不清楚   |
       | 0s       | 2.8s   | 取箭                   | 0s交接   |
       | 0.2s     | 3s     | 准备发射箭矢           | 准备发射 |
       | 0.5s     | 3.5s   | 发射箭矢               | 不清楚   |
   | 3s       | 6.5s   | 若没有投中，则继续取箭 | 人工装箭 |
      | 1s       | 7.5s   | 取箭、准备、发射       |          |
   | ...      | ...    | ...                    | ...      |
   
    3. R2流程（如果需要发射箭矢
   
       | 所需时间 | 时间点 | 备注                                   | 机构动作 |
       | -------- | ------ | -------------------------------------- | -------- |
       | 0s       | 0s     | 准备开始                               | 准备射箭 |
       | 0.3s     | 0.3s   | 开始射箭                               | 开始射箭 |
       | 0.5s     | 0.8s   | 箭矢发射完毕                           | 箭矢发射 |
       | 2.2s     | 3s     | 进入内区，配合R1发射                   | 不清楚   |
       | ns       | ns     | 此时R1由于有箭未中，需要进行下一步操作 |          |
2. R1与R2都发射
	1. R1流程

       | 所需时间 | 时间点 | 备注         | 机构动作 |
       | -------- | ------ | ------------ | -------- |
       | 0s       | 0s     | 准备开始     | 准备射箭 |
       | 0.3s     | 0.3s   | 开始射箭     | 开始射箭 |
       | 0.5s     | 0.8s   | 箭矢发射完毕 | 箭矢发射 |
       
   2. R2流程（发射箭矢，就不需要越障）

       | 所需时间 | 时间点 | 备注         | 机构动作 |
       | -------- | ------ | ------------ | -------- |
       | 0s       | 0s     | 准备开始     | 准备射箭 |
       | 0.3s     | 0.3s   | 底盘加速     | 电机加速 |
       | 1s       | 1.3s   | 移动到箭架处 | 不清楚   |
       | 0s       | 1.3s   | 0s交接取箭   | 不清楚   |
       | 0.5s     | 1.8s   | 准备发射     | 准备发射 |
       | 0.5s     | 2.3s   | 发射箭矢     | 发射箭矢 |

![image-20200912170337336](https://i.loli.net/2020/09/12/zoI3MbNac9nU8BY.png)

![img](https://i.loli.net/2020/09/13/S7fs1dltcH8qNIx.png)

### R1

发射机构数量 ：1， 2， 3， 4， 5 。。。。

发射机构需要可以调整发射方位和角度、发射速度

包含机构：发射机构，交接机构，底盘

#### 交接机构

某种巧妙的交接机构，类似于19年传接令牌的机构，设置两个把握住箭身。与发射机构相连接。

#### 发射机构

1. 电机

   1. 
    ![](https://i.loli.net/2020/09/13/8sbkwXxz3tj9DS2.png)
   2. 直线电机

2. 交接机构

   交接机构同时起到固定箭矢的作用，连接在发射器上
   
   ![image-20200913145129758](https://i.loli.net/2020/09/13/6X7fTh3kxz4d5wJ.png)


#### 底盘

舵轮底盘，可能需要找到合适的位置输出。发射时要锁死。

### R2

R2与R1的不同是需要干扰设计还有可能需要拾箭机构，发射机构与R1类似，可以不需要交接机构。

#### 机身设计

拦截箭是不是可以采用伞状结构

![image-20200913145531118](https://i.loli.net/2020/09/13/9yQeFGBnlv6hdDq.png)

#### 发射机构

与R1类似

#### 拾箭机构

拾箭机构如果太慢，就先不考虑拾取的事情。

#### 干扰机构

通过某种机构快速抓取把手，反复摇晃

#### 底盘

应该也是舵轮底盘
