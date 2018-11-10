# 挖矿

## 列出账户

personal.listAccounts

## 创建账户

web3.personal.newAccount("123456")

## 设置挖矿账户

eth.coinbase

miner.setEtherbase(eth.coinbase)

miner.setEtherbase(eth.accounts[0])

## 开始挖矿

> 可能需要设置启动项 --dev --dev.period 1

miner.start(1)

## 查看区块

eth.blockNumber

## 停止挖矿

miner.stop()
