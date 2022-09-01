# Chandy-Lamport 分布式快照

## 介绍

在本实验中，你将实现 Clandy-Lamport 分布式快照算法。

在开始实验前，你可能会考虑：节点怎么表示，网络怎么构建，事件行为如何产生，消息如何编码等等等等。但是，这些你都不用担心，因为分布式快照算法是构建在底层系统之上，为整个系统提供全局快照能力的。所以在实验中，也提供了一个底层系统：一个简单的 token 传递系统，其中的事件是 “节点 A 向 节点 B 转移 10 个 token”。

其中已经实现了关于 simulator、server、message 等实体的建模，也实现了普通的转账消息的传输方式，你需要先阅读代码和测试逻辑，在标有 `TODO: IMPLEMENT ME` 的代码段填充你的代码，以实现 Clandy-Lamport 分布式快照算法，实现系统的全局快照功能。

## 代码框架

在 src 目录下可以找到以下代码，为了使你能更快地进入到快照算法的内容，这里将对整个程序框架做一个说明：

##### test_data & test_common.go

test_data 中包含用例的输入和预期结果。

其中 .top 文件中是节点的初始信息和网络拓扑结构，.events 文件是过程中行为（事件）的序列，.snap 文件是期望得到的快照结果。

再结合 test_common.go 可以看到架构中是如何对以上文件进行处理，使用 .top 文件信息初始化节点和 .events 文件驱动事件。

##### simulator.go

Simulator 是整个框架的核心，其负责

* 初始化 server
* 初始化网络拓扑结构
* 驱动事件发生

##### server.go

表示分布式系统中的一个进程。其中包括 `SendTokens`、`StartSnapshot` 等方法

##### 辅助结构

`logger.go`：记录系统执行的事件

`common.go`：定义消息类型

`syncmap.go`：一个线程安全的 map 实现，可以不使用

`queue.go`：一个队列的简单实现



## 测试

测试代码位于 `snapshot_test.go`，测试用例位于 `test_data/`，要测试正确性，只需要运行：

```shell
$ cd chandy-lamp/ 
$ go test 
```

