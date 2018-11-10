# Running in Docker

> 注意


## install

We keep a Docker image with recent snapshot builds from the develop branch on DockerHub. 
In addition to the container based on Ubuntu (158 MB), 
there is a smaller image using Alpine Linux (35 MB). 
To use the alpine tag, replace ethereum/client-go with ethereum/client-go:alpine in the examples below.

```bash
docker pull ethereum/client-go
```

Start a node with:

```bash
docker run -it -p 30303:30303 ethereum/client-go
```

To start a node that runs the JSON-RPC interface on port 8545, run:

> WARNING: This opens your container to external calls. "0.0.0.0" should not be used when exposed to public networks

```bash
docker run -it -p 8545:8545 -p 30303:30303 ethereum/client-go --rpc --rpcaddr "0.0.0.0"
```

To use the interactive JavaScript console, run:

```bash
docker run -it -p 30303:30303 ethereum/client-go console
```

## Using Data Volumes

To persist downloaded blockchain data between container starts, 
use Docker data volumes. Replace /path/on/host with the location you want to store the data in.

```bash
docker run -it -p 30303:30303 -v /path/on/host:/root/.ethereum ethereum/client-go
```