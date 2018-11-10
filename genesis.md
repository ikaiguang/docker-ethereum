# genesis

genesis

## Defining the private genesis state

> 定义私人创世链

First, you'll need to create the genesis state of your networks, which all nodes need to be aware of
and agree upon. This consists of a small JSON file (e.g. call it genesis.json):

> 首先，您需要创建网络的起源状态，所有节点都需要了解并达成一致意见。这包含一个小的JSON文件（例如调用它genesis.json）：

```json
{
  "config": {
        "chainId": 0,
        "homesteadBlock": 0,
        "eip155Block": 0,
        "eip158Block": 0
    },
  "alloc"      : {},
  "coinbase"   : "0x0000000000000000000000000000000000000000",
  "difficulty" : "0x20000",
  "extraData"  : "",
  "gasLimit"   : "0x2fefd8",
  "nonce"      : "0x0000000000000042",
  "mixhash"    : "0x0000000000000000000000000000000000000000000000000000000000000000",
  "parentHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
  "timestamp"  : "0x00"
}
```

param

|参数名称|	参数描述|
| ----- | ----- |
|mixhash|	与nonce配合用于挖矿，由上一个区块的一部分生成的hash。注意他和nonce的设置需要满足以太坊的Yellow paper, 4.3.4. Block Header Validity, (44)章节所描述的条件。|
|nonce|	nonce就是一个64位随机数，用于挖矿，注意他和mixhash的设置需要满足以太坊的Yellow paper, 4.3.4. Block Header Validity, (44)章节所描述的条件。|
|difficulty|	设置当前区块的难度，如果难度过大，cpu挖矿就很难，这里设置较小难度|
|alloc|	用来预置账号以及账号的以太币数量，因为私有链挖矿比较容易，所以我们不需要预置有币的账号，需要的时候自己创建即可以。|
|coinbase|	矿工的账号，随便填|
|timestamp|	设置创世块的时间戳|
|parentHash|	上一个区块的hash值，因为是创世块，所以这个值是0|
|extraData|	附加信息，随便填，可以填你的个性信息|
|gasLimit|	该值设置对GAS的消耗总量限制，用来限制区块能包含的交易信息总和，因为我们是私有链，所以填最大。|

The above fields should be fine for most purposes, although we'd recommend changing the nonce to
some random value so you prevent unknown remote nodes from being able to connect to you. If you'd
like to pre-fund some accounts for easier testing, you can populate the alloc field with account
configs:

> 上述字段对于大多数用途应该没问题，但我们建议将其更改nonce为某个随机值，以防止未知的远程节点能够连接到您。
  如果您想预先为某些帐户提供资金以便于测试，您可以alloc使用帐户配置填充该字段：

```json
{
    "alloc": {
      "0x0000000000000000000000000000000000000001": {"balance": "100"},
      "0x0000000000000000000000000000000000000002": {"balance": "200"}
    }
}
```

run

|参数名称|参数描述|
| ----- | ----- |
|identity|区块链的标示，随便填写，用于标示目前网络的名字|
|init|指定创世块文件的位置，并创建初始块|
|datadir|设置当前区块链网络数据存放的位置|
|port|网络监听端口|
|rpc|启动rpc通信，可以进行智能合约的部署和调试|
|rpcapi|设置允许连接的rpc的客户端，一般为db,eth,net,web3|
|networkid|设置当前区块链的网络ID，用于区分不同的网络，是一个数字|
|console|启动命令行模式，可以在Geth中执行命令|
|nodiscover|私有链地址，不会被网上看到|
|...|...|

```bash
geth --identity "secbro etherum" \
    --rpc --rpccorsdomain "*" \
    --datadir "/home/zhuzs/eth/chain" \
    --port "30303" \
    --rpcapi "db,eth,net,web3" \
    -- networkid 95518 console --dev 
```

With the genesis state defined in the above JSON file, you'll need to initialize every Geth node
with it prior to starting it up to ensure all blockchain parameters are correctly set:

> 使用上述JSON文件中定义的genesis状态，您需要在启动它之前使用它初始化每个 Geth节点，以确保正确设置所有区块链参数：

```bash
geth init path/to/genesis.json
```

