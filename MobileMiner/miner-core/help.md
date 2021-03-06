---
title: MINER CORE
---
+ 依赖commonLibs
+ 定义与挖矿平台通用接口与utils
+ 连接矿池相关操作

## 温控设计
### 设计目的
MINER作为高耗能、高发热应用,必须对其作温度控制。若任由MINER全占用式的运行可能会导致如下危害。
+ 手机严重发热
+ 手机芯片性能下降(发热降频)
+ 电量急速损耗

不管发热还是性能下降都会严重影响用户的日常使用体验,用户可能为此直接卸载应用。

### 设计思路
1. 首先确定目标最高温度,该温度由外部引入
2. 每隔一段时间获取一次手机温度
3. 根据手机的温度,指定具体的操作
    1. 如果手机温度低于指定温度,设置线程数为cpu核数-1,cpu占用100%
    2. 如果手机温度高于指定温度,设置线程数为cpu核数-2,cpu占用80%