# RGB

 RGB协议的开发者开创了现代基于比特币的彩色币协议中使用的许多理念。RGB设计的主要要求之一是使协议与链下支付通道兼容（参见第318页的“支付通道和状态通道”），例如闪电网络（LN）中使用的通道。RGB协议的每一层都实现了这一点：

一次性密封 为了创建支付通道，Bob将他的彩色币分配给一个需要他和Alice双方签名才能花费的UTXO。他们对该UTXO的相互控制用作未来转移的一次性密封。

付款合约（P2C） Alice和Bob现在可以签署多个版本的P2C合约。底层支付通道的执行机制确保双方有动机只在链上发布最新版本的合约。

客户端验证 为了确保Alice和Bob都不需要相互信任，他们各自检查了所有彩色币的历史转移，直到其创建，以确保所有合约规则都被正确遵循。

RGB的开发人员已经描述了他们的协议的其他用途，例如创建可以定期更新以防止私钥泄露的身份令牌。

欲了解更多信息，请参阅[RGB的文档](https://rgb.tech/)。
