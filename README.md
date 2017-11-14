# Install-Bitcoin-core-Ubuntu
How to install Bitcoin core @Ubuntu

## Reference:

> http://www.jianshu.com/p/3767b20856c6

> https://bitcoin.org/en/developer-examples#regtest-mode
            
## There are two ways to install
### 1, You can download the install package from [bitcoin.org](https://bitcoin.org/en/download)
### 2, Also you can install it with PPA( We will talk about this way )
#### Install
##### 1, Enter:

    sudo add-apt-repository ppa:bitcoin/bitcoin
> Your system will fetch the PPA's key. This enables your Ubuntu system to verify that the packages in the PPA have not been interfered with since they were built.


##### 2, Enter:

    sudo apt-get update  
> Your system will pull down the latest list of Bitcoin core from each archive it knows about.  

##### 3, Enter:
 
     sudo apt-get install bitcoind  
> Install Bitcoind  

##### 4, Enter:

    sudo apt-get install bitcoin-qt  
> This step is **not necessary**. If you are running ubuntu-desktop, you may wanna use bitcoin-qt. If you are running ubuntu-service, there is no need to install bitcoin-qt.  
#### Run & check

    bitcoind
> Running *bitcoind* foreground

    bitcoind -daemon
> Running *bitcoind* background

    bitcoin-cli getinfo
> You can check your bitcoind process. It may looks like

    {
      "version": 120100,
      "protocolversion": 70012,
      "walletversion": 60000,
      "balance": 0.00000000,
      "blocks": 32,
      "timeoffset": 0,
      "connections": 6,
      "proxy": "",
      "difficulty": 1,
      "testnet": false,
      "keypoololdest": 1472539508,
      "keypoolsize": 101,
      "paytxfee": 0.00000000,
      "relayfee": 0.00001000,
      "errors": ""
    }
> You can also check ***debug.log***

    cd $HOME/.bitcoin
    tail -f debug.log

#### Configuration

*bitcoind* is more useful for programming: it provides a full peer which you can interact with through RPCs to port 8332 (or 18332 for testnet).

*bitcoin-cli* allows you to send RPC commands to bitcoind from the command line.

When you use command ***ll*** in direction *$HOME/.bitcoin*, there are some files. Such us:

+ **bitcoind.pid**   *bitcoind运行的进程文件*
+ **blocks**   *区块链数据文件*
+ **chainstate**   *区块链状态的数据库使用LevelDB存储*
+ **db.log**   *数据库日志文件*
+ **debug.log**   *运行时的日志文件*
+ **wallet.dat**   *钱包文件*

To use *bitcoind* and *bitcoin-cli*, you will need to add a RPC password to your **bitcoin.conf** file.

In direction *$HOME/.bitcoin*, you can enter:

    vi bitcoin.conf
    i
    rpcpassword=change_this_to_a_long_random_password
    :wq

Now enter this for check:

    bitcoind -regtest -daemon

It will show:

    Bitcoin server starting

You can create a private block chain by:

**Bitcoin Core 0.10.1 and earlier**
    bitcoin-cli -regtest setgenerate true 101

**Bitcoin Core master (as of commit 48265f3)**
    bitcoin-cli -regtest generate 101

Now enter this for check:

    bitcoin-cli -regtest getbalance

It will show:

    50.00000000

