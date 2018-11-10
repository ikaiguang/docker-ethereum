# Mac installation options

## Installing with Homebrew

By far the easiest way to install go-ethereum is to use our Homebrew tap. 
If you don't have Homebrew, install it first.

Then run the following commands to add the tap and install geth:

```bash
brew tap ethereum/ethereum
brew install ethereum
```

You can install the develop branch by running --devel:

```bash
brew install ethereum --devel
```

After installing, run geth account new to create an account on your node.

You should now be able to run geth and connect to the network.

Make sure to check the different options and commands with geth --help

For options and patches, see: https://github.com/ethereum/homebrew-ethereum

## Building from source

Building Geth (command line client)

Clone the repository to a directory of your choosing:

```bash
git clone https://github.com/ethereum/go-ethereum
```

Building geth requires some external libraries to be installed:

- GMP
- Go

```bash
brew install gmp go
```

Finally, build the geth program using the following command.

```bash
cd go-ethereum
make geth
```

You can now run build/bin/geth to start your node.