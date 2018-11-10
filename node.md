# node

私有节点

## 网络

```bash

# network
docker network create --subnet 172.200.0.0/16 ethereum-node

```

## 添加节点

```text

admin.addPeer("enode://node_id@ip:port")

```

## 其他

```bash

# log
docker logs -f ethereum-node-1

# exec
docker exec -it ethereum-node-1 /bin/sh

# restart
docker restart ethereum-node-1

# remove
docker rm -f ethereum-node-1

```

> 查看节点信息
  
```bash

# 连接节点
geth attach http://127.0.0.1:8545

# 其他连接示例
# geth attach ipc:<datadir>/geth.ipc
# geth attach ws://191.168.1.1:8546

# 节点id
admin.nodeInfo.enode

# 添加节点
# admin.addPeer("enode://....")
# (ifconfig); (ifconfig|grep netmask|awk '{print $2}'); (ip a)
admin.addPeer

# 节点信息
net.listening
net.peerCount
admin.peers

# 账户
eth.accounts

# 余额
# eth.getBalance()
eth.getBalance

```

## 静态节点

```bash
touch <datadir>/static-nodes.json
```

```json

[
  "enode://f4642fa65af50cfdea8fa7414a5def7bb7991478b768e296f5e4a54e8b995de102e0ceae2e826f293c481b5325f89be6d207b003382e18a8ecba66fbaf6416c0@33.4.2.1:30303",
  "enode://pubkey@ip:port"
]

```

## 开机重启 && 服务挂掉重启

1. docker 启动所有节点 (docker run -itd --restart=always ...)
2. 进入 docker 容器 (docker exec -it container_id /bin/sh)
3. 查看 ip (ifconfig) (ip a)
4. 连接 ethereum (geth attach http://127.0.0.1:8545)
5. 查看节点信息 (admin.nodeInfo.enode)
6. 创建节点信息文件 (touch <datadir>/static-nodes.json)
7. 输出节点信息 (\["enode://pubkey@ip:port","enode://pubkey@ip:port",...])
8. 重启 docker (docker restart container_id ...)

## 重启

```bash

docker rm -f ethereum-node-1 ethereum-node-2 ethereum-node-3
rm -rf ./cluster_node1/ethereum_data
rm -rf ./cluster_node2/ethereum_data
rm -rf ./cluster_node3/ethereum_data

# cd node1 node2 node3
docker run --rm -it \
    -v $(pwd)/ethereum_conf:/ethereum_conf \
    -v $(pwd)/ethereum_data:/ethereum_data \
    ethereum/client-go \
    --datadir "/ethereum_data" \
    init /ethereum_conf/genesis.json

# restart node
    
docker restart ethereum-node-1 ethereum-node-2 ethereum-node-3

# stop
docker stop ethereum-node-1 ethereum-node-2 ethereum-node-3


```

