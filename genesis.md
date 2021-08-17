# 创世区块

## 什么是创世文件

创世文件定义了`CSC`的初始状态，我们可能通过高度为`0`的区块进行查看。`CSC`第一个区块是从`1`开始，其父区块即为创世区块。`CSC`为了方便用户操作，将创世区块直接集成到二进制包`cetd`，我们在搭建节点的时候无需下载，如果对创世区块感兴趣可以通过[github](https://github.com/coinex-smart-chain/csc)下载并查看。如果有人想用`CSC`搭建自己的链，可以定制修改创世文件，参考[搭建私链](node_private_chain.md)。

以下将对创世文件里面的相关参数进行解释。

## 参数解释

* chainId - 链标识
  * `CSC`主网：`52`
  * `CSC`测试网：`53`

* senatus - `CSC`共识配置
  * period - 出块时间，`CSC`为3秒
  * epoch - 验证节点集合更新区块间隔数，`CSC`为200个区块数

* nonce - 由于`CSC`设置为`0x0`
* timestamp - 区块时间
* extraData - 包含是三部分数据
  * 前32byte作为签名用户预留的固定数据
  * 验证节点地址
  * 出块节点签名，末尾65byte
* gasLimit - 区块运行的gas限制
* difficulty - 到目前为止的区块难度
* coinbase - 出块节点地址
* alloc - 预分配的地址
* number - 区块高度，创世区块为`0`
* parentHash - 当前区块的父区块hash，创世区块为`0`
