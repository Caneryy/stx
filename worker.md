# Stx faz 2 kurulum

-----------------------------------------------

değiştir yazan yerleri dosyada aratarak değiştirin.
Toplam 8 yeri değiştirmiş olun.

-----------------------------------------------

sudo adduser testnet

sudo visudo

root    ALL=(ALL:ALL) ALL 
olan satırı bul altına bu satırı ekle 
testnet ALL=(ALL:ALL) ALL

CTRL+O enter CTRL+X yaparak kaydet ve çık.

-----------------------------------------------

sudo su - testnet

sudo apt-get update

sudo apt-get install build-essential

sudo apt-get install libtool autotools-dev autoconf 

sudo apt-get install libssl-dev 

sudo apt-get install libboost-all-dev 

sudo add-apt-repository ppa:luke-jr/bitcoincore

sudo apt-get update 

sudo apt-get install bitcoind

-----------------------------------------
```
mkdir ~/.bitcoin/
cd ~/.bitcoin/
nano bitcoin.conf
```
aşağıdakini yapıştır

-----------------------------------------------
```
server=1
rpcuser=değiştirUSERNAME
rpcpassword=değiştirPASSWORD
testnet=1
txindex=0
listen=1
rpcserialversion=0
maxorphantx=1
banscore=1

[test]
bind=0.0.0.0:18333
rpcbind=0.0.0.0:18332
rpcport=18332
rpcallowip=0.0.0.0/0
rpcallowip=::/0
rpcallowip=127.0.0.1
```
-------------------------------------------------

CTRL + O, ENTER, CTRL + X yaparak kaydet ve çık.

-------------------------------------------------

tmux new -s session1

bitcoind -conf=/home/testnet/.bitcoin/bitcoin.conf

CTRL + B sonrada D'ye basarak sessionı aşağı al.

tmux attach -t session1 
komutu ile tekrardan içine girebilirsin.

tmux ls

bitcoin-cli getblockchaininfo 
bu komut ile kontrol et ortalama yarım saat sürüyor. 

-----------------------------------------------

bitcoin-cli -rpcport=18332 -rpcuser=değiştirYUKARDAYAZDIĞINUSERNAME -rpcpassword=değiştirYUKARDAYAZDIĞINPASSWORD importaddress değiştirOLUŞTURDUĞUNBTCADRESI

bu işlem 10 dakikaya kadar sürebiliyor.

-----------------------------------------------

sudo apt-get install build-essential cmake libssl-dev pkg-config

curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

source $HOME/.cargo/env

-----------------------------------------------

git clone https://github.com/blockstack/stacks-blockchain.git; cd stacks-blockchain

cargo build --workspace --release --bin stacks-node

bu işlem 15 dakikaya kadar sürebiliyor.

-----------------------------------------------

cd testnet/stacks-node/conf/

nano testnet-miner-conf.toml

aşağıdaki kısmı içine yapıştır.

-----------------------------------------------
```
[node]
rpc_bind = "0.0.0.0:20443"
p2p_bind = "0.0.0.0:20444"
bootstrap_node = "047435c194e9b01b3d7f7a2802d6684a3af68d05bbf4ec8f17021980d777691f1d51651f7f1d566532c804da506c117bbf79ad62eea81213ba58f8808b4d9504ad@xenon.blockstack.org:20444"
seed = "değiştirJSONDAKI PRIVATE KEY"
miner = true
pox_sync_sample_secs = 1

[burnchain]
chain = "bitcoin"
mode = "xenon" # if connecting to Krypton, set this to "krypton"
peer_host = "127.0.0.1"
username = "değiştirYUKARDA YAZDIĞIN USERNAME"
password = "değiştirYUKARDA BELIRLEDIĞIN PASSWORD"
rpc_port = 18332
peer_port = 18333
burnchain_op_tx_fee = 11000
burn_fee_cap = 20000

[[ustx_balance]]
address = "STB44HYPYAT2BB2QE513NSP81HTMYWBJP02HPGK6"
amount = 10000000000000000
[[ustx_balance]]
address = "ST11NJTTKGVT6D1HY4NJRVQWMQM7TVAR091EJ8P2Y"
amount = 10000000000000000
[[ustx_balance]]
address = "ST1HB1T8WRNBYB0Y3T7WXZS38NKKPTBR3EG9EPJKR"
amount = 10000000000000000
[[ustx_balance]]
address = "STRYYQQ9M8KAF4NS7WNZQYY59X93XEKR31JP64CP"
amount = 10000000000000000
```
-----------------------------------------------

CTRL + O, ENTER, CTRL + X yaparak kaydet ve çık.

-----------------------------------------------

cd ~/stacks-blockchain/target/release

tmux new -s session2

./stacks-node start --config=/home/testnet/stacks-blockchain/testnet/stacks-node/conf/testnet-miner-conf.toml

-----------------------------------------------

HAYIRLI OLSUN
