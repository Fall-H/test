# Coinbase交易

 在任何区块中，第一个交易都是一笔特殊的交易，称为coinbase交易。这笔交易由Jing的节点构建，并支付他挖矿所获得的奖励。

Jing的节点将coinbase交易创建为对自己钱包的支付。Jing收集的挖矿奖励总额是区块补贴（2023年为6.25个新比特币）和包含在区块中的所有交易的交易费用之和。

与常规交易不同，coinbase交易不消耗（花费）UTXO作为输入。相反，它只有一个输入，称为coinbase输入，隐含包含区块奖励。coinbase交易必须至少有一个输出，并且可以有尽可能多的输出，以适应区块。在2023年的coinbase交易中，常见的是有两个输出：其中一个是使用OP\_RETURN的零值输出，用于承诺区块中所有隔离见证（segwit）交易的所有见证。另一个输出支付矿工的奖励。

 