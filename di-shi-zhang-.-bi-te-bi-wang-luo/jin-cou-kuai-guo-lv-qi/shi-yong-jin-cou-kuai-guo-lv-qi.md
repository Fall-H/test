# 使用紧凑块过滤器

 每个区块中对输出脚本的每个承诺的64位值被排序，重复的条目被移除，并且通过查找每个条目之间的差值（增量）来构建GCS。然后，对等方将该紧凑块过滤器分发给它们的客户（如钱包）。

客户端使用这些增量来重建原始的承诺。客户端，比如钱包，还会对其监视的所有输出脚本进行相同方式的承诺生成，就像BIP158那样。它检查它生成的任何承诺是否与过滤器中的承诺匹配。

回想一下，紧凑块过滤器失真类似于截断数字的情况。想象一个客户端正在寻找一个包含数字123456的区块，而一个准确（但失真）的紧凑块过滤器包含数字1234。当一个客户端看到1234时，它将下载相关的区块。准确的过滤器包含1234的情况下，客户端学习到包含123456的区块的概率是100%，称为真正的正匹配。然而，该区块可能还包含123400、123401或近百个其他不符合客户端期望的条目（在这个例子中），称为假正匹配。

一个100%的真正匹配率是很好的。这意味着一个钱包可以依赖紧凑块过滤器来找到影响该钱包的每个交易。非零的假正匹配率意味着钱包将下载一些对其无兴趣的区块。这的主要后果是客户端会使用额外的带宽，这不是一个很大的问题。BIP158紧凑块过滤器的实际假正匹配率非常低，因此这不是一个主要问题。假正匹配率也可以帮助提高客户端的隐私，就像布隆过滤器一样，尽管任何想要最佳隐私的人仍然应该使用自己的完整节点。

长期来看，一些开发者主张让区块对该区块的过滤器进行承诺，最可能的方案是每个Coinbase交易对该区块的过滤器进行承诺。完整节点将为每个区块计算过滤器，并仅在包含准确承诺的情况下接受该区块。这将允许轻量级客户端下载一个80字节的区块头、一个（通常很小的）Coinbase交易和该区块的过滤器，以获得强有力的证据证明该过滤器是准确的。
