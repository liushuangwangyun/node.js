# node.js

## 第二天笔记

## 异步式IO

什么是异步：

例子：同步：CPU需要计算10个数据，没计算一个结果后，将其写入磁盘，等待写入成功后，再计算下一个数据，知道完成

异步：CPU需要计算十个数据，每计算一个结果后，将其写入磁盘，不等待写入成功与否的结果，立刻返回继续计算下一个数据，

计算过程中可以收到之前写入是否成功的通知，知道完成。

（1）至少在两个对象之间需要协作

（2）两个对象都需要处理一系列的事情，
