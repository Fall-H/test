# 输入脚本字段

 输入脚本字段是遗留交易格式的残余。我们的示例交易输入花费了一个不需要输入脚本中的任何数据的本地隔离见证输出，因此输入脚本的长度前缀设置为零（0x00）。

对于一个长度前缀的输入脚本示例，它花费了一个遗留输出，我们使用了一个在此书撰写时的最新区块中的任意交易： 6b483045022100a6cc4e8cd0847951a71fad3bc9b14f24d44ba59d19094e0a8c fa2580bb664b020220366060ea8203d766722ed0a02d1599b99d3c95b97dab8e 41d3e4d3fe33a5706201210369e03e2c91f0badec46c9c903d9e9edae67c167b 9ef9b550356ee791c9a40896

长度前缀是一个紧凑型无符号整数，表示序列化的输入脚本字段的长度。在这种情况下，它是一个字节（0x6b），表示输入脚本为107字节。我们将在第7章详细介绍解析和使用脚本。
