# NOMP KawPoW Algorithm Pool -HiveCoin
Highly Efficient mining pool for Coins based on KawPoW algo!

This is opensource mining pool for HiveCoin, Please visit [HiveCoin](https://www.hivecoin.org) for more information

### Example site
[Hiveminer.eu](http://hiveminer.eu/stats/hivecoin)

-------
### Screenshots
#### Home<br />
![Home](https://raw.githubusercontent.com/Satoex/kawpow-pool/master/docs/frontend/home.png)

#### Pool Stats<br />
![Pool Stats](https://raw.githubusercontent.com/Satoex/kawpow-pool/master/docs/frontend/poolstats.png)<br /><br />

#### Miner Stats<br />
![Miner Stats](https://raw.githubusercontent.com/Satoex/kawpow-pool/master/docs/frontend/minerstats.png)<br /><br />

#### Payments<br />
![Payments](https://raw.githubusercontent.com/Satoex/kawpow-pool/master/docs/frontend/payments.png)<br /><br />

-------
### Node Open Mining Portal consists of 3 main modules:
| Project | Link |
| ------------- | ------------- |
| [KawPoWNOMP](https://github.com/HiveProject2021/kawpow-pool) | https://github.com/HiveProject2021/kawpow-pool |
| [Stratum Pool](https://github.com/dr4mohamed/kawpow-stratum-pool-1.git) | https://github.com/dr4mohamed/kawpow-stratum-pool-1.git |
| [Node Multihashing](https://github.com/dr4mohamed/node-multi-hashing.git) | https://github.com/dr4mohamed/node-multi-hashing.git |

-------
### Requirements
***NOTE:*** _These requirements will be installed in the install section!_<br />
* Ubuntu Server 18.04.* LTS
* Coin daemon
* Node Version Manager
* Node 8.1.4
* Process Manager 2 / pm2
* Redis Server
* ntp

-------

### Install HiveCoin Daemon

    adduser pool
    usermod -aG sudo pool
    su - pool
    sudo apt install wget
    wget https://github.com/HiveProject2021/Hivecoin/releases/download/4.2.3.5.2/hivecoin4.3.2.5.deb
    sudo dpkg -i hivecoin4.3.2.5.deb
    mkdir -p ~/.hive/
    touch ~/.hive/hive.conf
    echo "rpcuser=user1" > ~/.hive/hive.conf
    echo "rpcpassword=pass1" >> ~/.hive/hive.conf
    echo "prune=550" >> ~/.hive/hive.conf
    echo "daemon=1" >> ~/.hive/hive.conf
    ./hived
    ./hive-cli getnewaddress

Example output: HNRMPAYzdBHGWgK7CjSFByuUcufCHSST7r - it is the address of your pool, you need to remember it and specify it in the configuration file pool_configs/hivecoin.json.
    
    ./hive-cli getaddressesbyaccount ""
    
Information about pool wallet address.
    
    ./hive-cli getwalletinfo
    
Get more information.

    ./hive-cli getblockcount
    
Information about synchronization of blocks in the main chain.

    ./hive-cli help
Other helpfull commands.

-------

### Install Pool

    sudo apt install git -y
    cd ~
    git config --global http.https://gopkg.in.followRedirects true
    git clone https://github.com/HiveProject2021/kawpow-pool
    cd kawpow-pool/
    ./install.sh

-------
### Configure Pool

Change "stratumHost": "192.168.0.200", to your IP or DNS in file config.json:

    cd ~/kawpow-pool
    nano config.json

```javascript
{
    
    "poolname": "Hive Coin Pool",
    
    "devmode": false,
    "devmodePayMinimim": 0.25,
    "devmodePayInterval": 120,
    
    "logips": true,       
    "anonymizeips": true,
    "ipv4bits": 16,
    "ipv6bits": 16,
    "poolwarningmsg": "",
    
    "defaultCoin": "hivecoin",
    
    "poollogo": "/static/icons/hivecoin.png",
    
    "discordtwitterfacebook": "",
    
    "pagetitle": "Hive Coin Pool - 0% Fees Promo",
    "pageauthor": "Hive project",
    "pagedesc": "A reliable, 0% fee, easy to use mining pool for cryptocurrency! No matter your experience with mining cryptocurrency, we make it easy! Get started mining today!",
    "pagekeywds": "GPU,CPU,Hash,Hashrate,Cryptocurrency,Crypto,Mining,Pool,Bitcoin,Hive,Hivecoin,Wavi,Wavicoin,Dixicoin,Dixi,QBic,QBicCoin,Easy,Simple,How,To",

    "btcdonations": "",
    "ltcdonations": "",
    "ethdonations": "",

    "logger" : {
        "level" : "debug",
        "file" : "./logs/nomp_debug.log"
    },

    "cliHost": "127.0.0.1",
    "cliPort": 17117,

    "clustering": {
        "enabled": false,
        "forks": "auto"
    },

    "defaultPoolConfigs": {
        "blockRefreshInterval": 1000,
        "jobRebroadcastTimeout": 55,
        "connectionTimeout": 600,
        "emitInvalidBlockHashes": false,
        "validateWorkerUsername": true,
        "tcpProxyProtocol": false,
        "banning": {
            "enabled": true,
            "time": 600,
            "invalidPercent": 50,
            "checkThreshold": 500,
            "purgeInterval": 300
        },
        "redis": {
            "host": "127.0.0.1",
            "port": 6379
        }
    },

    "website": {
        "enabled": true,
        "sslenabled": false,
        "sslforced": false,
        "host": "0.0.0.0",
        "port": 8080,
        "sslport": 443,
        "sslkey": "~/nomp-kawpow-pool/certs/privkey.pem",
        "sslcert": "~/nomp-kawpow-pool/certs/fullchain.pem",
        "stratumHost": "192.168.100.105",
        "stats": {
            "updateInterval": 30,
            "historicalRetention": 172800,
            "hashrateWindow": 600
        },
        "adminCenter": {
            "enabled": false,
            "password": "NOT_WORKING_YET_:P_LESHACAT_CAN_DO_ADMIN_PANEL_FUNCTIONALITY_TOO"
        }
    },

    "redis": {
        "host": "127.0.0.1",
        "port": 6379
    },

    "switching": {
        "switch1": {
            "enabled": false,
            "algorithm": "sha256",
            "ports": {
                "3333": {
                    "diff": 10,
                    "varDiff": {
                        "minDiff": 16,
                        "maxDiff": 512,
                        "targetTime": 15,
                        "retargetTime": 90,
                        "variancePercent": 30
                    }
                }
            }
        },
        "switch2": {
            "enabled": false,
            "algorithm": "scrypt",
            "ports": {
                "4444": {
                    "diff": 10,
                    "varDiff": {
                        "minDiff": 16,
                        "maxDiff": 512,
                        "targetTime": 15,
                        "retargetTime": 90,
                        "variancePercent": 30
                    }
                }
            }
        },
        "switch3": {
            "enabled": false,
            "algorithm": "x11",
            "ports": {
                "5555": {
                    "diff": 0.001,
                    "varDiff": {
                        "minDiff": 0.001,
                        "maxDiff": 1, 
                        "targetTime": 15, 
                        "retargetTime": 60, 
                        "variancePercent": 30 
                    }
                }
            }
        }
    },

    "profitSwitch": {
        "enabled": false,
        "updateInterval": 600,
        "depth": 0.90,
        "usePoloniex": true,
        "useCryptsy": true,
        "useMintpal": true,
        "useBittrex": true
    }

}
```
Create a pool config for you coins:
    
    cp pool_configs/hivecoin_example.json pool_configs/hivecoin.json

Change "address": "HQWTiHTAUVxUkrV72bqW5Tfrpgbzkde1Q4", to your pool created wallet address in file ravencoin.json:

    cd pool_configs
    nano hivecoin.json

```javascript
{
    "enabled": true,
    "coin": "hivecoin.json",

    "address": "HQWTiHTAUVxUkrV72bqW5Tfrpgbzkde1Q4",
    
    "donateaddress": "HQWTiHTAUVxUkrV72bqW5Tfrpgbzkde1Q4",

    "rewardRecipients": {
	    "HNRMPAYzdBHGWgK7CjSFByuUcufCHSST7r":0.5
    },

    "paymentProcessing": {
        "enabled": true,
        "schema": "PROP",
        "paymentInterval": 300,
        "minimumPayment": 5,
        "maxBlocksPerPayment": 50000,
        "minConf": 30,
        "coinPrecision": 8,
        "daemon": {
            "host": "127.0.0.1",
            "port": 9766,
            "user": "user1",
            "password": "pass1"
        }
    },

    "ports": {
		"10001": {
            "diff": 0.001,
    	    "varDiff": {
    	        "minDiff": 0.001,
    	        "maxDiff": 32,
    	        "targetTime": 10,
    	        "retargetTime": 60,
    	        "variancePercent": 30,
    		    "maxJump": 25
    	    }
        },
		"10002": {
            "diff": 0.01,
    	    "varDiff": {
    	        "minDiff": 0.01,
    	        "maxDiff": 32,
    	        "targetTime": 10,
    	        "retargetTime": 60,
    	        "variancePercent": 30,
    		    "maxJump": 25
    	    }
        },
		"10003": {
            "diff": 0.1,
    	    "varDiff": {
    	        "minDiff": 0.1,
    	        "maxDiff": 32,
    	        "targetTime": 10,
    	        "retargetTime": 60,
    	        "variancePercent": 30,
    		    "maxJump": 25
    	    }
        },
		"10004": {
            "diff": 0.5,
    	    "varDiff": {
    	        "minDiff": 0.5,
    	        "maxDiff": 32,
    	        "targetTime": 10,
    	        "retargetTime": 60,
    	        "variancePercent": 30,
    		    "maxJump": 25
    	    }
        },
		"10005": {
            "diff": 1,
    	    "varDiff": {
    	        "minDiff": 1,
    	        "maxDiff": 32,
    	        "targetTime": 10,
    	        "retargetTime": 60,
    	        "variancePercent": 30,
    		    "maxJump": 25
    	    }
        },
		"10006": {
            "diff": 2,
    	    "varDiff": {
    	        "minDiff": 2,
    	        "maxDiff": 32,
    	        "targetTime": 10,
    	        "retargetTime": 60,
    	        "variancePercent": 30,
    		    "maxJump": 25
    	    }
        },
		"10007": {
            "diff": 4,
    	    "varDiff": {
    	        "minDiff": 4,
    	        "maxDiff": 64,
    	        "targetTime": 10,
    	        "retargetTime": 60,
    	        "variancePercent": 30,
    		    "maxJump": 25
    	    }
        },
		"10008": {
            "diff": 0.5,
    	    "varDiff": {
    	        "minDiff": 0.5,
    	        "maxDiff": 32,
    	        "targetTime": 10,
    	        "retargetTime": 60,
    	        "variancePercent": 30,
    		    "maxJump": 25
    	    }
        }
    },

    "daemons": [
        {
            "host": "127.0.0.1",
            "port": 9766,
            "user": "user1",
            "password": "pass1"
        }
    ],

    "p2p": {
        "enabled": false,
        "host": "127.0.0.1",
        "port": 19333,
        "disableTransactions": true
    },

    "mposMode": {
        "enabled": false,
        "host": "127.0.0.1",
        "port": 3306,
        "user": "me",
        "password": "mypass",
        "database": "ltc",
        "checkPassword": true,
        "autoCreateWorker": false
    },

    "mongoMode": {
        "enabled": false,
        "host": "127.0.0.1",
        "user": "",
        "pass": "",
        "database": "ltc",
        "authMechanism": "DEFAULT"
    }

}

```

### Run Pool
    
    node ./init.js

