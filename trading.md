# 交易

基本交易

> 其他

```bash

# 进入docker
docker exec -it ethereum-node-1 /bin/sh

# 连接节点
geth attach http://127.0.0.1:8545

```

## 查询账户

```bash

# 命令1
eth.accounts

# 命令2
web3.eth.accounts

```

## 创建账户

```text

# 此命令创建账户，会导致docker退出（重启docker）
# personal.newAccount("password")

# 推荐使用这个创建账户
web3.personal.newAccount("123456")

```

## 查询余额

```text

# 命令1
eth.getBalance(eth.accounts[0])
eth.getBalance("0x0000000000000000000000000000000000000001")
eth.getBalance("account")

# 命令2
web3.eth.getBalance(eth.accounts[0])

# 命令3
web3.fromWei(eth.getBalance("account"), "ether")

```

## 单位

wei : 1 eth = 1000000000000000000 wei

```text

# 单位转换
web3.toWei(0.05, "ether")
web3.fromWei(eth.getBalance("account"), "ether")
web3.fromWei(eth.getBalance("0x0000000000000000000000000000000000000001"), "ether")

```

> 1 eth = 10 的 18 次方 wei

## 初始化的账户

```text

# 账户1
eth.getBalance("0x0000000000000000000000000000000000000001")

# 账户2
eth.getBalance("0x0000000000000000000000000000000000000002")


```

## 转账

```text

# 解锁
personal.unlockAccount(eth.accounts[0], "123456")


# 转账
eth.sendTransaction({from:sender, to:receiver, value: amount})
eth.sendTransaction({from:eth.coinbase, to:eth.accounts[1], value: web3.toWei(0.05, "ether")})
eth.sendTransaction({from:eth.accounts[0], to:eth.accounts[2], value: web3.toWei(0.1, "ether")})
web3.eth.sendTransaction({from:eth.accounts[0], to:eth.accounts[1], value: web3.toWei(0.1, "ether")})
web3.eth.sendTransaction({from:eth.accounts[0], to:"0xc44341572692f46ef670be83a4cc1ad78fc5f216", value: web3.toWei(0.1, "ether")})

# 查询
eth.getBalance(eth.accounts[0])
eth.getBalance("0xc44341572692f46ef670be83a4cc1ad78fc5f216")

```

## 交易状态查询

> https://ethereum.stackexchange.com/questions/6002/transaction-status/6003#6003

```text



# 查询交易
eth.getTransaction("0x525fe4acd3ef3b48f5b28ddac26993964fd57964b32ed2c41347d12780d804e0")

# 查询收据
eth.getTransactionReceipt("0x525fe4acd3ef3b48f5b28ddac26993964fd57964b32ed2c41347d12780d804e0")

# 查询挂起来的交易
eth.getBlock("pending").transactions

# 挂起的交易 blockNumber = null.
eth.getTransaction(eth.getBlock("pending").transactions[0])
{
  blockHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
  blockNumber: null,
  from: "0x90e440e8b7bb0ccc780b614c75956d475cef16a3",
  gas: 90000,
  gasPrice: 1000000000,
  hash: "0x8df2df96902119e3e690a7c70b1daf5a71984c863ccf1567a78b768923702491",
  input: "0x",
  nonce: 0,
  r: "0xdba08030540b4def3f539ec57ff20a7c73af797d8601428e75b4e352bcbe8071",
  s: "0x526a42580e69453ea346f145d052dc197b4330b03ceca37bfeb767b25892e445",
  to: "0x7c6262d1b3d8db591bafa71b716e44b5b298c669",
  transactionIndex: 0,
  v: "0x11a018c5",
  value: 100000000000000000
}

# 成功的交易
eth.getBlock("latest").transactions

# 查询成功的交易
eth.getTransaction(eth.getBlock("latest").transactions[1])

```
