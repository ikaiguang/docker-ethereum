# docker-ethereum

> 搭建 docker 的 ethereum 节点

- ethereum [ethereum.md](ethereum.md)
- 单独的节点 [alone_node/readme.md](alone_node/readme.md)
- 集群 
    + [cluster_node1/readme.md](cluster_node1/readme.md) 
    + [cluster_node2/readme.md](cluster_node2/readme.md) 
    + [cluster_node3/readme.md](cluster_node3/readme.md)
- 测试数据 [test_data.md](test_data.md)
- docker [docker.md](docker.md)
- docker-composer [docker-compose.yml.example](docker-compose.yml.example)
- 集群小窍门 [node.md](node.md)
- api [api.md](api.md)
- 交易 [trading.md](trading.md)
- 挖矿 [mining.md](mining.md)
- GPU [gpu.md](gpu.md)
- genesis [genesis.md](genesis.md)
- genesis.json [genesis.json.example](genesis.json.example)
- static-nodes.json [static-nodes.json.example](static-nodes.json.example)

## docker 版本

> docker version

- client version : 18.06.1-ce
- server version : 18.06.1-ce

## ethereum version

```bash

docker run --rm -it ethereum/client-go version

```

Version: 1.8.18-unstable

## 工作目录

本人使用golang编程，所以：目录设置为 $GOPATH/src/github.com/ikaiguang/docker-ethereum

你可以自定义工作目录

```bash

cd path/to/your_path

git clone https://github.com/ikaiguang/docker-ethereum.git

# work path
cd path/to/your_path/docker-ethereum

```

## docker 网络

```bash

docker network create --subnet 172.200.0.0/16 ethereum-node

```

## 单独的节点

```bash

# docker 网路
docker network create --subnet 172.200.0.0/16 ethereum-node

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

## 集群之前 ：添加测试数据（可跳过）

```bash

# work path
cd $GOPATH/src/github.com/ikaiguang/docker-ethereum/cluster_node1

# 创建账户 1
docker run --rm -it \
    -v $(pwd)/ethereum_conf:/ethereum_conf \
    -v $(pwd)/ethereum_data:/ethereum_data \
    ethereum/client-go \
    --datadir "/ethereum_data" \
    account new
    
# 创建账户 2
docker run --rm -it \
    -v $(pwd)/ethereum_conf:/ethereum_conf \
    -v $(pwd)/ethereum_data:/ethereum_data \
    ethereum/client-go \
    --datadir "/ethereum_data" \
    account new
    
# 修改所有节点的 ethereum_conf 目录下的 genesis.json 文件的 alloc 地址为创建的两个地址

90e440e8b7bb0ccc780b614c75956d475cef16a3
7c6262d1b3d8db591bafa71b716e44b5b298c669

```

## 集群

搭建 3 个节点的集群

1. docker 网络

```bash

# docker 网路
docker network create --subnet 172.200.0.0/16 ethereum-node

```

2. 启动节点1

```bash

# work path
cd $GOPATH/src/github.com/ikaiguang/docker-ethereum/cluster_node1

# init genesis.json
docker run --rm -it \
    -v $(pwd)/ethereum_conf:/ethereum_conf \
    -v $(pwd)/ethereum_data:/ethereum_data \
    ethereum/client-go \
    --datadir "/ethereum_data" \
    init /ethereum_conf/genesis.json

# start
docker run -itd --restart=always \
    --name ethereum-node-1 \
    --network ethereum-node --ip 172.200.0.31 \
    -v $(pwd)/ethereum_conf:/ethereum_conf \
    -v $(pwd)/ethereum_data:/ethereum_data \
    -p "18545:18545" \
    -p "18546:18546" \
    -p "10303:10303" \
    ethereum/client-go \
    --datadir "/ethereum_data" \
    --identity "node1" \
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

```

3. 启动节点2

```bash

# work path
cd $GOPATH/src/github.com/ikaiguang/docker-ethereum/cluster_node2

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

```

4. 启动节点3

```bash

# work path
cd $GOPATH/src/github.com/ikaiguang/docker-ethereum/cluster_node3

# init genesis.json
docker run --rm -it \
    -v $(pwd)/ethereum_conf:/ethereum_conf \
    -v $(pwd)/ethereum_data:/ethereum_data \
    ethereum/client-go \
    --datadir "/ethereum_data" \
    init /ethereum_conf/genesis.json

# start
docker run -itd --restart=always \
    --name ethereum-node-3 \
    --network ethereum-node --ip 172.200.0.33 \
    -v $(pwd)/ethereum_conf:/ethereum_conf \
    -v $(pwd)/ethereum_data:/ethereum_data \
    -p "48545:18545" \
    -p "48546:18546" \
    -p "40303:10303" \
    ethereum/client-go \
    --datadir "/ethereum_data" \
    --identity "node3" \
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

```

5. 进入集群中节点记录 nodeInfo

```bash

# 节点1
docker exec -it ethereum-node-1 /bin/sh
geth attach http://127.0.0.1:18545
admin.nodeInfo.enode

# 节点2
docker exec -it ethereum-node-2 /bin/sh
geth attach http://127.0.0.1:18545
admin.nodeInfo.enode

# 节点3
docker exec -it ethereum-node-3 /bin/sh
geth attach http://127.0.0.1:18545
admin.nodeInfo.enode

```

6. 创建静态节点文件 `static-nodes.json`

> 节点id，ip地址，端口必须对应 ： "enode://节点id@ip地址:端口"

```json

[
  "enode://1e9f4506fb9462fdcf33ae2a7af681324b1e97f033a4bffbb4a3263ce3739d7c144fa8e0406b54be90155550a1720f66360d053027ba7279a47e299384cb754f@172.200.0.31:10303",
  "enode://9f9c3a79a6d2c00abb15d0ecfaa38cd4b73b070380f52388c27a6a814f5720f8d68659290913dd392a080e356773c982a45b1d178fb647afaa179a1c4645b3cf@172.200.0.32:10303",
  "enode://99f7bb708dae6890221dfee0e22cecf4c27af7f14f341001b12d83a9b6cb1c16b2950b7cdfb8000d5fcad5407252754ec20386eef8c9e6d47885436c6f4ea888@172.200.0.33:10303"
]

```

7. 复制 `static-nodes.json` 到节点数据目录

```bash

cp static-nodes.json $GOPATH/src/github.com/ikaiguang/docker-ethereum/cluster_node1/ethereum_data
cp static-nodes.json $GOPATH/src/github.com/ikaiguang/docker-ethereum/cluster_node2/ethereum_data
cp static-nodes.json $GOPATH/src/github.com/ikaiguang/docker-ethereum/cluster_node3/ethereum_data

```

8. 重启节点

```bash

docker restart ethereum-node-1 ethereum-node-2 ethereum-node-3

```
