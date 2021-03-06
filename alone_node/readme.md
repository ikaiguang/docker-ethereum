# 单独的节点

一个测试的节点

## docker 网络

```bash

docker network create --subnet 172.200.0.0/16 ethereum-node

```

## 单独的节点

```bash

# 工作目录
cd $GOPATH/src/github.com/ikaiguang/docker-ethereum

# 节点目录
cd alone_node

# 启动
docker run -itd --restart=always \
    --name ethereum-node \
    --network ethereum-node --ip 172.200.0.30 \
    -v $(pwd)/ethereum_conf:/ethereum_conf \
    -v $(pwd)/ethereum_data:/ethereum_data \
    -p "58545:18545" \
    -p "58546:18546" \
    -p "50303:10303" \
    ethereum/client-go \
    --datadir "/ethereum_data" \
    --identity "node1" \
    --nodiscover \
    --dev --dev.period 1 \
    --networkid 147852369 \
    --ipcdisable \
    --rpcport 18545 \
    --wsport 18546 \
    --port 10303 \
    --verbosity 6 \
    --rpc --rpcaddr "0.0.0.0" \
    --rpccorsdomain "*" \
    --rpcapi "eth,net,web3,rpc,admin,personal,clique,debug,miner,shh,txpool" \
    console
    
# 自动挖矿 ： --dev --dev.period 1
# 限制 rpc api 选项 ： --rpcapi "db,eth,net,web3,personal,admin"
# modules: admin:1.0 clique:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 shh:1.0 txpool:1.0 web3:1.0

```

> 其他

```bash

# log
docker logs -f ethereum-node

# exec
docker exec -it ethereum-node /bin/sh

# restart
docker restart ethereum-node

# remove
docker rm -f ethereum-node

```

> 节点操作

```bash

# 连接节点

# docker 容器内
geth attach http://127.0.0.1:18545

# 宿主机
geth attach http://127.0.0.1:58545

# 其他连接示例
# geth attach ipc:<datadir>/geth.ipc
# geth attach ws://191.168.1.1:18546

# 节点id
admin.nodeInfo.enode

# 添加节点
# admin.addPeer("enode://node_id@ip:port")
# (ifconfig); (ifconfig|grep netmask|awk '{print $2}'); (ip a)
admin.addPeer

# 节点信息
net.listening
net.peerCount
admin.peers

# 账户
eth.accounts

# 余额
eth.getBalance

```