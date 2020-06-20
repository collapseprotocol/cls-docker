# Go version for CLS

Golang implementation of the collapse protocol with a docker version. 

# Description of collapse protocol
As Bitcoin plays the role of gold as reserve, CLS will act as the dollar in the future. How would this happen? Imagine BTC as gold so it has similar cons as gold. The transaction is slow so it can not be used as daily settlement. The circulation supply is so limited that if settlement volume increases the supply will not be enough. The world needs a better system like the dollar and the system will get adoption as dollar domination the world.

The important conclusion we discovered from the story of the dollar is that we have to begin with “gold” as reserve and then the system will have its robustness at the beginning. Once it grows big enough then it is time to expand and finally replace “gold” as the settlement layer. The collapse phase is designed to collect the “reserve - Bitcoin '' when we first start CLS platform so with BTC converted at a fixed rate we can accumulate enough BTC as the fundamentals of the system. When the fundamentals are steadily built then it is time to start phase II: the expansion. The adoption will be a natural thing since the circulation supply and time-lapse from Bitcoin is not good enough people will settle in CLS.

# INSTALL

+ ubuntu 18 operating system preferred, also support other Linux based os
+ install basic software such as docker.io etc..
    ```
    sudo apt update
    sudo apt install -y docker.io && sudo apt install -y docker-compose
    sudo apt install -y make
    ```
+ modify /etc/docker/daemon.json, set the max log size to avoid some disk errors
    ```
    {
        "log-opts":{ "max-size" :"100m","max-file":"1"}
    }
    ```
+ clone the code
    ```
    git clone https://github.com/collapseprotocol/cls-docker.git
    cd cls-docker
    sudo make run
    ```

# USAGE

## Run as MasterNode

For masternode, we should create a private key for mining, then import it to wallet.
```
cd data
echo ${your private key} >> pri.pri
sudo ../bin/dpeth --datadir . account import pri.pri
# input ${passphase} by following tips
echo ${passphase} > pass
rm -f pri.pri
```

After importing, we should replace the miner address to our addr:
```
cd ../

# modify 0x8d8C4f9B8f8b2c94F021E2e7D93fEEA45e58726D to ${your miner addr} which just imported
vi docker-compose.yaml
```

Restart it, then would run correctly if the miner addr has been the masternode:
```
make run  # will recreating the container automatically
```

## Run as FullNode

FullNode is a regular node which just sync the blockchain headers && data, and will not miner any blocks.

To run it as fullnode, you should just comment the masternode section, and uncomment the "common node use" section, then run:
```
make run  # will recreating the container automatically
```

it will synchronize automatically now.

# Contact

If you want any further information, feel free to contact us at  **cls@collapseprotocol.io**
