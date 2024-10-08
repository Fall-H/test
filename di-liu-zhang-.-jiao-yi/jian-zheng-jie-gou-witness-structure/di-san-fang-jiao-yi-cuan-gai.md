# 第三方交易篡改

一个更复杂的交易系列有时可以消除循环依赖，但是许多协议随后会遇到一个新的问题：通常可以用不同的方式解决相同的脚本。例如，考虑我们从“见证结构”中的简单脚本：

 2 OP\_ADD 4 OP\_EQUAL

我们可以通过在输入脚本中提供值2来使此脚本通过，但在比特币中有几种方法可以将该值放入堆栈中。以下只是其中几种方式：

OP\_2&#x20;

OP\_PUSH1 0x02&#x20;

OP\_PUSH2 0x0002&#x20;

OP\_PUSH3 0x000002

&#x20;...&#x20;

OP\_PUSHDATA1 0x0102&#x20;

OP\_PUSHDATA1 0x020002&#x20;

...&#x20;

OP\_PUSHDATA2 0x000102&#x20;

OP\_PUSHDATA2 0x00020002&#x20;

...&#x20;

OP\_PUSHDATA4 0x0000000102&#x20;

OP\_PUSHDATA4 0x000000020002&#x20;

...

 每种对数字2在输入脚本中的替代编码都会生成一个略有不同的交易，具有完全不同的交易ID（txid）。每个不同版本的交易都花费了与其他版本相同的输入（outpoint），使它们彼此冲突。在有效的区块链中，一组冲突交易只能包含其中的一个版本。

想象一下，Alice创建了一个在输入脚本中带有OP\_2的交易版本，并有一个输出支付给Bob。然后Bob立即将该输出花费给了Carol。任何网络上的人都可以用OP\_PUSH1 0x02替换OP\_2，与Alice的原始版本产生冲突。如果那个冲突的交易得到确认，那么就没有办法将Alice的原始版本包含在同一区块链中，这意味着Bob的交易无法花费其输出。尽管Alice、Bob和Carol都没有做错任何事情，但Bob向Carol的付款变得无效了。某人（第三方）能够改变（突变）Alice的交易，这就是所谓的不受欢迎的第三方交易篡改问题。

{% hint style="info" %}
有些情况下，人们希望他们的交易是可篡改的，比特币提供了几个功能来支持这一点，其中最重要的是我们将在“签名哈希类型（SIGHASH）”中学到的签名哈希（sighash）。例如，Alice可以使用签名哈希允许Bob帮助她支付一些交易费用。这会改变Alice的交易，但只以Alice想要的方式。因此，我们有时会在术语“交易可篡改性”前加上“不受欢迎的”一词。即使我们和其他比特币技术撰写者使用更短的术语，我们几乎肯定是在谈论不受欢迎的篡改变体。
{% endhint %}
