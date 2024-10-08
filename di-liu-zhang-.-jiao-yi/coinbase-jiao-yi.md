# Coinbase交易

每个区块中的第一笔交易都是一个特例。大多数较旧的文档称之为生成交易，但大多数较新的文档称之为Coinbase交易（不要与名为“Coinbase”的公司创建的交易混淆）。

Coinbase交易是由包含它们的区块的矿工创建的，允许矿工领取该区块中所有交易支付的任何费用。此外，在区块6,720,000之前，矿工被允许领取一笔由以前从未流通过的比特币组成的补贴，称为区块补贴。矿工可以领取的区块的总金额——包括费用和补贴——称为区块奖励。 Coinbase交易的一些特殊规则包括：

* 它们只能有一个输入。
* 单个输入的输出点必须具有空的txid（完全由零组成）和最大的输出索引（0xffffffff）。这样做是为了防止Coinbase交易引用先前的交易输出，因为Coinbase交易支付费用和补贴，引用先前的交易输出至少会令人困惑。
* 在普通交易中包含输入脚本的字段称为coinbase。正是这个字段赋予了Coinbase交易其名称。coinbase字段的长度必须至少为两个字节，但不超过100个字节。虽然此脚本不会执行，但是对于签名检查操作（sigops）的传统交易限制仍然适用，因此应在其中放置的任意数据应以数据推送操作码为前缀。自2013年BIP34定义的一个软分叉以来，此字段的前几个字节必须遵循我们将在“Coinbase数据”中描述的其他规则。
* 输出的总和不得超过区块中所有交易所收取的费用和补贴的价值。补贴从每个区块的50个比特币开始，每210,000个区块减半一次（大约每四年）。补贴值会向下舍入到最近的satoshis。
* 自2017年在BIP141中记录的segwit软分叉以来，包含消费segwit输出的交易的任何区块都必须包含一个输出到Coinbase交易的输出，该输出承诺该区块中所有交易（包括它们的见证）。我们将在第12章探讨这种承诺。 Coinbase交易可以具有任何在普通交易中有效的其他输出。但是，在Coinbase交易获得100次确认之前，消费其中一笔输出的交易不能包含在任何区块中。这称为成熟规则，尚未获得100次确认的Coinbase交易输出称为未成熟。 大多数比特币软件不需要处理Coinbase交易，但它们的特殊性质意味着它们偶尔可能会导致未经设计以接受它们的软件出现异常问题。

 