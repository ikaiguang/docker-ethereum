# 节点 2

## 网络

```bash

# network
docker network create --subnet 172.200.0.0/16 ethereum-node

```

## 启动

```bash

# work path
cd $GOPATH/src/github.com/ikaiguang/docker-ethereum

# node path
cd cluster_node2

# init genesis.json
docker run --rm -it \
    -v $(pwd)/ethereum_conf:/ethereum_conf \
    -v $(pwd)/ethereum_data:/ethereum_data \
    ethereum/client-go \
    --datadir "/ethereum_data" \
    init /ethereum_conf/genesis.json

# start
docker run -itd --restart=always \
    --name ethereum-node-2 \
    --network ethereum-node --ip 172.200.0.32 \
    -v $(pwd)/ethereum_conf:/ethereum_conf \
    -v $(pwd)/ethereum_data:/ethereum_data \
    -p "28545:18545" \
    -p "28546:18546" \
    -p "20303:10303" \
    ethereum/client-go \
    --datadir "/ethereum_data" \
    --identity "node2" \
    --nodiscover \
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
    
# 私有 ： --nodiscover
# 限制 rpc api 选项 ： --rpcapi "db,eth,net,web3,personal,admin"
# modules: admin:1.0 clique:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 shh:1.0 txpool:1.0 web3:1.0

```

> 其他

```bash

# log
docker logs -f ethereum-node-2

# exec
docker exec -it ethereum-node-2 /bin/sh

# restart
docker restart ethereum-node-2

# remove
docker rm -f ethereum-node-2

```

> 节点操作

```bash

# 连接节点

# docker 容器内
docker exec -it ethereum-node-2 /bin/sh
geth attach http://127.0.0.1:18545

# 宿主机
geth attach http://127.0.0.1:28545

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