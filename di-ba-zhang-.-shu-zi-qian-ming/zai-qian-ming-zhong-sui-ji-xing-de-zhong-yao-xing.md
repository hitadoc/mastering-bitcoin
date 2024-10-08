# 在签名中随机性的重要性

正如我们在“Schnorr Signatures”（第187页）和“ECDSA Signatures”（第197页）中所看到的，签名生成算法使用一个随机数k作为私有/公有nonce对的基础。k的值并不重要，只要它是随机的。如果来自同一个私钥的签名使用了私有nonce k并且对不同的消息（交易）进行签名，那么签名私钥可以被任何人计算出来。在签名算法中重复使用相同的值k会导致私钥曝光！

{% hint style="danger" %}
如果在两笔不同交易上的签名算法中使用相同的值k，那么私钥就可以被计算并暴露给世界！
{% endhint %}

这不仅仅是一种理论可能性。我们曾经看到这个问题导致比特币中几种不同实现的交易签名算法暴露私钥。由于意外重用k值，人们的资金被盗。重用k值的最常见原因是随机数生成器未正确初始化。

为了避免这种漏洞，业界最佳实践是不仅使用熵进行种子初始化的随机数生成器生成k，而是使用部分由交易数据本身加上正在使用的私钥进行种子初始化的过程。这确保了每个交易产生不同的k。确定k的行业标准算法是在RFC6979中定义的，由互联网工程任务组发布。对于schnorr签名，BIP340建议了一个默认的签名算法。

 BIP340和RFC6979可以完全确定性地生成k，这意味着相同的交易数据将始终产生相同的k。许多钱包采用这种方法，因为这样可以轻松编写测试来验证其关键安全签名代码是否正确生成k值。BIP340和RFC6979都允许在计算中包含附加数据。如果该数据是熵，则即使签署了完全相同的交易数据，也会产生不同的k。这可以增加对侧信道和故障注入攻击的防护。

如果您正在实现比特币交易签名算法，您必须使用BIP340、RFC6979或类似的算法，以确保为每个交易生成不同的k。

 