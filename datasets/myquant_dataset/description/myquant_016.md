# 行业轮动(股票)

分享

阅读 91216
 更新 2022-05-09 16:56:48

* [行业轮动策略](#0154de37d02116fa)
  + [1. 原理](#4d68e06c45acd2a2)
    - [行业轮动现象](#a8e1628d8676e515)
    - [行业轮动的原因](#e1d8c185f9839e8e)
    - [行业轮动下资产配置](#ce741e7a54261bed)
  + [2. 策略思路](#cf0127fe1bcb3311)
  + [3. 策略代码](#69a3fc437f0227e3)
  + [4. 回测结果分析与稳健性检验](#2a39edb4bd1fa9ab)

# 行业轮动策略

## 1. 原理

### 行业轮动现象

在某一段时间内，某一行业或某几个行业组内股票价格共同上涨或下降的现象。

行业轮动策略是根据行业轮动现象做成的策略，利用行业趋势进行获利的方法，属于主动交易策略。其本质是通过一段时期的市场表现，力求抓住表现较好的行业以及投资品种，选择不同时期的强势行业进行获利。

### 行业轮动的原因

***原因1：行业周期***

行业的成长周期可以分为初创期、成长期、成熟期和衰退期，一般行业会按照这个周期运行。初创期属于行业刚刚起步阶段，风险高、收益小。成长期内风险高、收益高。处于成熟期的企业风险低、收益高。处于衰退期的企业风险低、收益低。在一段时间内，不同的行业会处于不同的行业周期，在时间维度上看会呈现行业轮动现象。

***原因2：国家政策***

国家政策对我国资本市场有重大影响。我国每年的财政政策和货币政策都是市场关注的热点，货币政策和财政政策会释放出影响市场的信息，如利率。当政策释放出下调利率的信号，就为资金需求量大、项目周期长的行业缓解了压力，如房地产行业，这时对于这类行业利好，相应的股价就会上涨。

***原因3：重大事件***

资本市场对于消息的反应是迅速的。根据有效市场理论，在半强式有效市场下，一切已公开的信息都会反映在股价当中。以疫情为例，消息一出迅速拉动医疗行业股价水平，带动行业增长。

### 行业轮动下资产配置

**1. 美林时钟：大类资产配置**

根据经济增长和通货膨胀可以将经济分为四个周期：衰退、复苏、过热、滞涨。

美林时钟分析了四个不同时期，并总结出适合投资的资产类别。

| 周期阶段 | 经济增长 | 通货膨胀 | 最优资产类别 | 最优股票板块 |
| --- | --- | --- | --- | --- |
| 衰退 | 下降 | 下降 | 债券 | 防御成长 |
| 复苏 | 上升 | 下降 | 股票 | 周期成长 |
| 过热 | 上升 | 上升 | 商品 | 周期价值 |
| 滞涨 | 下降 | 上升 | 现金 | 防御价值 |

研究宏观经济时主要关注两个变量：GDP和CPI。

其中GDP选择不变价（剔除通货膨胀的影响），关心同比值差分后的符号。如果同比值>0，差分后仍然>0，说明GDP在加速上涨；如果同比值<0,差分后仍然<0，说明GDP在加速下跌。

**当经济增长速度加快时，与国家经济联系紧密的行业如钢铁、煤炭、电力等基建利润也会随之增长。**

**当经济增速放缓是，非周期性的行业如医药、基础消费品、基础建设等行业呈现较强的防御性。**

**当通货膨胀处于较低水平时，市场利率水平也处于较低水平。按照股票估值理论，此时的折现率处于低水平，价格相对而言较高。此时，金融行业的股价会呈现明显的上涨。**

**当通货膨胀处于较高水平时，市场利率较高，此时现金为王，原材料价格走高。与此相关的原材料行业就会表现较好，如天然气、石油等。**

**2. 策略设计**

**行业动量策略**

部分研究表明，行业在日、月频率上会存在动量现象，在周频率上会存在反转现象，也就是行业间轮动。因此，在日和月频率上可以利用行业动量设计策略，如果是在周频率上可以利用反转效应设计策略。  
（引自：武文超. 中国A股市场的行业轮动现象分析——基于动量和反转交易策略的检验[J]. 金融理论与实践, 2014, 000(009):111-114.）

**行业因子策略**

将行业变量作为一个因子放入多因子模型中，利用多因子模型预测各个行业的周期收益率，采用滚动预测方法每次得到一个样本外预测值，根据这些预测值判断该买入哪些行业，卖出哪些行业。  
（引自：高波, 任若恩. 基于主成分回归模型的行业轮动策略及其业绩评价[J]. 数学的实践与认识, 2016, 46(019):82-92.）

## 2. 策略思路

策略示例采用第一种策略构建方法，利用行业动量设计策略。为了提高策略速度，以6个行业为例进行演示。

第一步：确定行业指数，获取行业指数收益率。  
第二步：根据行业动量获取最佳行业指数。  
第三步：在最佳行业中，选择最大市值的5支股票买入。

回测时间：2017-07-01 08:00:00 到 2017-10-01 16:00:00  
回测标的：SHSE.000910.SHSE.000909.SHSE.000911.SHSE.000912.SHSE.000913.SHSE.000914  
(300工业.300材料.300可选.300消费.300医药.300金融)  
回测初始资金：1000万

## 3. 策略代码

```