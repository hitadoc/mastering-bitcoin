# 加密和认证连接

 大多数新用户认为比特币节点的网络通信是加密的。事实上，比特币的原始实现完全以明文通信，截至撰写本文时，现代的比特币核心实现也是如此。&#x20;

为了增加比特币P2P网络的隐私和安全性，有一种解决方案提供了通信加密：Tor传输。&#x20;

Tor是一项软件项目和网络，通过随机的网络路径提供数据的加密和封装，从而实现匿名性、不可追踪性和隐私性。&#x20;

比特币核心提供了几种配置选项，允许您在Tor网络上传输比特币节点的流量。此外，比特币核心还可以提供Tor隐藏服务，允许其他Tor节点通过Tor直接连接到您的节点。&#x20;

从比特币核心版本0.12开始，如果节点能够连接到本地Tor服务，它将自动提供一个隐藏的Tor服务。如果您已经安装了Tor，并且比特币核心进程以具有足够权限访问Tor身份验证cookie的用户身份运行，它应该会自动工作。使用调试标志来启用比特币核心的Tor服务调试，像这样：

```css
$ bitcoind --daemon --debug=tor
```

您应该在日志中看到“tor: ADD\_ONION successful”，表示比特币核心已将一个隐藏服务添加到Tor网络中。&#x20;

您可以在比特币核心文档（docs/tor.md）和各种在线教程中找到有关将比特币核心作为Tor隐藏服务运行的更多说明。

 