# ethereum

## geth是什么

go-ethereum就是通常所说的 geth 
它是一个用Go语言实现运行在以太坊完整节点上的命令行接口，
安装并运行了geth，你可以成为以太坊正式链的节点并且可以：

- 挖矿得到真实的以太币
- 在账户地址之间转移资金
- 创建智能合约和发起交易
- 查看所有历史区块
- ......

## 客户端种类

|客户端|语言|开发者|最新版本|
|-----|---|-----|-------|
|go-ethereum|Go|以太坊基金会|go-ethereum-v1.4.9|
|Parity|Rust|Ethcore|Parity-v1.2.1|
|cpp-ethereum|C++|以太坊基金会|cpp-ethereum-v1.2.9|
|pyethapp|Python|以太坊基金会|pyethapp-v1.2.3|
|ethereumjs-lib|Javascript|以太坊基金会|ethereumjs-lib-v3.0.0|
|Ethereum(J)|Java|<ether.camp>|ethereumJ-v1.3.0-RC3-daoRescue2|
|ruby-ethereum|Ruby|Jan Xie|ruby-ethereum-v0.9.3|
|ethereumH|Haskell|BlockApps|尚无Homestead 版本|

## 使用go-ethereum

1. git clone https://github.com/ethereum/go-ethereum
2. cd go-ethereum 
3. make geth
4. build/bin/geth

> 注意需要安装好go

## 使用docker

docker pull ethereum/client-go

## 启动节点

下面的命令行是加入以太坊ropsten测试网络，并且对外开放公网IP

```bash
nohup go-ethereum/build/bin/geth \
    --testnet \
    --rpc \
    --rpcaddr 0.0.0.0 \
    --rpcapi eth,net,web3 \
    --syncmode fast \
    --cache 1028 \
    --datadir /data/block/ > /data/block/geth.log 2>&1 &
```

- testnet (Ropsten network: pre-configured proof-of-work test network)
- rpc (Enable the HTTP-RPC server)
- rpcaddr (HTTP-RPC server listening interface (default: “localhost”))
- rpcapi (API’s offered over the HTTP-RPC interface)
- rpcport (HTTP-RPC server listening port (default: 8545))
- port (Network listening port (default: 30303))
- datadir (Data directory for the databases and keystore)
- syncmode (Blockchain sync mode (“fast”, “full”, or “light”))
- cache value (Megabytes of memory allocated to internal caching (min 16MB / database forced) (default: 128)) 优化性能
