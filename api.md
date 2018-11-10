# api 函数

geth version

```text

Geth
Version: 1.8.17-stable
Architecture: amd64
Protocol Versions: [63 62]
Network Id: 1
Go Version: go1.11.1
Operating System: darwin
GOPATH=/Users/kaiguang/golang
GOROOT=/usr/local/go

```

modules: admin:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0

## eth

```text

eth._requestManager            eth.getAccounts                eth.getRawTransaction          eth.mining                     
eth.accounts                   eth.getBalance                 eth.getRawTransactionFromBlock eth.namereg                    
eth.blockNumber                eth.getBlock                   eth.getStorageAt               eth.pendingTransactions        
eth.call                       eth.getBlockNumber             eth.getSyncing                 eth.protocolVersion            
eth.chainId                    eth.getBlockTransactionCount   eth.getTransaction             eth.resend                     
eth.coinbase                   eth.getBlockUncleCount         eth.getTransactionCount        eth.sendIBANTransaction        
eth.compile                    eth.getCode                    eth.getTransactionFromBlock    eth.sendRawTransaction         
eth.constructor                eth.getCoinbase                eth.getTransactionReceipt      eth.sendTransaction            
eth.contract                   eth.getCompilers               eth.getUncle                   eth.sign                       
eth.defaultAccount             eth.getGasPrice                eth.getWork                    eth.signTransaction            
eth.defaultBlock               eth.getHashrate                eth.hashrate                   eth.submitTransaction          
eth.estimateGas                eth.getMining                  eth.iban                       eth.submitWork                 
eth.filter                     eth.getPendingTransactions     eth.icapNamereg                eth.syncing                    
eth.gasPrice                   eth.getProtocolVersion         eth.isSyncing   

```

## personal

```text

personal._requestManager personal.ecRecover       personal.importRawKey    personal.lockAccount     personal.sendTransaction personal.unlockAccount   
personal.constructor     personal.getListAccounts personal.listAccounts    personal.newAccount      personal.sign            
personal.deriveAccount   personal.getListWallets  personal.listWallets     personal.openWallet      personal.signTransaction 

```

## admin

```text

admin.addPeer              admin.getDatadir           admin.nodeInfo             admin.sleepBlocks          admin.toString             
admin.addTrustedPeer       admin.getNodeInfo          admin.peers                admin.startRPC             admin.valueOf              
admin.clearHistory         admin.getPeers             admin.propertyIsEnumerable admin.startWS              
admin.constructor          admin.hasOwnProperty       admin.removePeer           admin.stopRPC              
admin.datadir              admin.importChain          admin.removeTrustedPeer    admin.stopWS               
admin.exportChain          admin.isPrototypeOf        admin.sleep                admin.toLocaleString

```

## debug

```text

debug.backtraceAt                 debug.getModifiedAccountsByNumber debug.setGCPercent                debug.traceBlock                  
debug.blockProfile                debug.goTrace                     debug.setHead                     debug.traceBlockByHash            
debug.chaindbCompact              debug.hasOwnProperty              debug.setMutexProfileFraction     debug.traceBlockByNumber          
debug.chaindbProperty             debug.isPrototypeOf               debug.stacks                      debug.traceBlockFromFile          
debug.constructor                 debug.memStats                    debug.startCPUProfile             debug.traceTransaction            
debug.cpuProfile                  debug.metrics                     debug.startGoTrace                debug.valueOf                     
debug.dumpBlock                   debug.mutexProfile                debug.stopCPUProfile              debug.verbosity                   
debug.freeOSMemory                debug.preimage                    debug.stopGoTrace                 debug.vmodule                     
debug.gcStats                     debug.printBlock                  debug.storageRangeAt              debug.writeBlockProfile           
debug.getBadBlocks                debug.propertyIsEnumerable        debug.toLocaleString              debug.writeMemProfile             
debug.getBlockRlp                 debug.seedHash                    debug.toString                    debug.writeMutexProfile           
debug.getModifiedAccountsByHash   debug.setBlockProfileRate         debug.traceBadBlock           

```

## miner

```text

miner.constructor          miner.isPrototypeOf        miner.setExtra             miner.start                miner.toString             
miner.getHashrate          miner.propertyIsEnumerable miner.setGasPrice          miner.stop                 miner.valueOf              
miner.hasOwnProperty       miner.setEtherbase         miner.setRecommitInterval  miner.toLocaleString       

```

## net

```text

net._requestManager net.getListening    net.getVersion      net.peerCount       
net.constructor     net.getPeerCount    net.listening       net.version 

```

## rpc

```text

rpc.constructor          rpc.hasOwnProperty       rpc.modules              rpc.toLocaleString       rpc.valueOf              
rpc.getModules           rpc.isPrototypeOf        rpc.propertyIsEnumerable rpc.toString         

```

## txpool

```text

txpool.constructor          txpool.getInspect           txpool.inspect              txpool.status               txpool.valueOf              
txpool.content              txpool.getStatus            txpool.isPrototypeOf        txpool.toLocaleString       
txpool.getContent           txpool.hasOwnProperty       txpool.propertyIsEnumerable txpool.toString             


```

## web3

```text

Array                Math                 TypeError            console              eval                 net                  toLocaleString       
BigNumber            NaN                  URIError             constructor          hasOwnProperty       parseFloat           toString             
Boolean              Number               Web3                 debug                inspect              parseInt             txpool               
Date                 Object               XMLHttpRequest       decodeURI            isFinite             personal             undefined            
Error                RangeError           _setInterval         decodeURIComponent   isNaN                propertyIsEnumerable unescape             
EvalError            ReferenceError       _setTimeout          encodeURI            isPrototypeOf        require              valueOf              
Function             RegExp               admin                encodeURIComponent   jeth                 rpc                  web3                 
Infinity             String               clearInterval        escape               loadScript           setInterval          
JSON                 SyntaxError          clearTimeout         eth                  miner                setTimeout 

```