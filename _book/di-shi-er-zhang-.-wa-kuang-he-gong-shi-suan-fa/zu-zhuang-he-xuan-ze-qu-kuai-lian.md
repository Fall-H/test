# 组装和选择区块链

比特币的去中心化共识机制的最后一部分是将区块组装成链，并选择具有最多工作量证明的链。 最佳的区块链是具有最多累积工作量证明的所有有效区块链。

_最佳链_也可能有与最佳链上的区块“同级”的分支。这些区块是有效的，但不是最佳链的一部分。它们被保留供将来参考，以防这些次要链中的任何一个后来成为主要链。当出现同级区块时，通常是由于在相同高度几乎同时挖掘不同区块造成的。&#x20;

当收到一个新区块时，节点将尝试将其添加到现有的区块链上。节点将查看区块的“上一个区块哈希”字段，该字段是指向区块父级的引用。然后，节点将尝试在现有的区块链中找到该父级。大多数情况下，父级将是最佳链的“尖端”，这意味着这个新区块扩展了最佳链。&#x20;

有时，新区块并不会扩展最佳链。在这种情况下，节点将新区块的头部连接到一个次要链上，然后将次要链的工作与先前的最佳链进行比较。如果次要链现在是最佳链，节点将相应地重新组织其已确认交易和可用UTXO的视图。如果节点是矿工，它现在将构建一个候选区块，扩展这个新的，具有更多工作量证明的链。&#x20;

通过选择具有最大累积工作量的有效链，所有节点最终达成网络范围内的共识。随着更多的工作被添加，最终解决了链之间的临时差异，从而扩展了可能的链。

{% hint style="info" %}
本节中描述的区块链分叉是由全球网络中的传输延迟自然发生的结果。我们也将在本章后面看到故意引发的分叉
{% endhint %}

 分叉几乎总是在一个区块内解决的。如果两个区块几乎同时被位于前一个分叉的相反“方向”的矿工发现，那么意外的分叉可能会延伸到两个区块。然而，这种情况发生的几率很低。

比特币的区块间隔为10分钟，是快速确认时间和分叉概率之间的设计妥协。更快的区块时间会使交易似乎更快得到确认，但会导致区块链分叉更频繁，而更慢的区块时间会减少分叉的数量，但使结算速度看起来更慢。

{% hint style="info" %}
哪种更安全：一个交易包含在平均每10分钟一个区块的区块中，还是一个交易包含在已建立在其上的九个区块的区块中，平均每个区块之间的时间是一分钟？答案是它们同样安全。想要进行双重支付的恶意矿工需要做的工作量与总网络算力的10分钟相等，以创建具有相同工作证明的链。

区块之间时间缩短并不意味着更早的结算。它的唯一好处是为那些愿意接受这些保证的人提供更弱的保证。例如，如果你愿意接受矿工在三分钟内就同意了最佳区块链作为足够的安全性，那么你会更喜欢一个每分钟一个区块的系统，你可以等待三个区块，而不是一个每10分钟一个区块的系统。区块之间的时间越短，越容易因意外分叉而浪费矿工的工作量（除其他问题外），因此许多人更喜欢比特币的10分钟区块而不是更短的区块间隔。
{% endhint %}
