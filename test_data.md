# 测试数据

需要虚拟数据进行测试

## 办法 1

使用单独节点并开启自动挖矿 --dev --dev.period 1

## 办法 2

> https://github.com/ethereum/go-ethereum/issues/14831

i think you can do it easier than this. before you run init, and with an empty datadir run

here is part of a script i am developing to set up a private node

```text

# wipe the old blockchain and wallet/keystore
rm -rf datadir 
mkdir datadir

# first we create some accounts
geth --datadir=./datadir --password ./password.txt account new > account1.txt
geth --datadir=./datadir --password ./password.txt account new > account2.txt

# update genesis json to use the addresses from one of the new accounts
<script here modifies genesis.json to replace the account ids with the just generated ones>

# create the blockchain with the fund allocations
geth --datadir ./datadir init genisis.json

```

## 办法 3

> https://github.com/ethereum/go-ethereum/issues/14831

```text

As the Fatal says， you have inited, so can't init again, try as following
1、start your geth and create a new account
2、write down the address, and copy the corresponding private key file under datadir/keystore/privatekeyfile. The private key file name like this UTC--2017-07-10T16-55-52.479148210Z--6e423da3705daaa16a3cdef560293139bb277a3e
3、remove the data dir
4、modify your genesis.json, replace the account and then init again
5、move the private key file to the newcreating datadir/keystore/ 

```

## 办法 4

```text

# first we create some accounts
geth --datadir=./datadir account new
    follow from the prompt, type and retype a passphrase, you will receive a result address, e.g. 
      address: {e44f98b12f1460bfde940f3b1bf95b537dbc4106}

# use any text editor to save the text below and save as genesis.json. Note the account address returned above is put in alloc:

```