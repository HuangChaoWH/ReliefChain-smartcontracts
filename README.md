# ReliefChain-smartcontract
ReliefChain (AngelHack SG June 2018) - C++ based EOS.IO smartcontract
### DAPP based on eos.io blockchain, solving natural disaster management issues such as distribution of rations, tracking missing people, double spending of ration and collaboration between various NGOs.

### Staring local blockchain/Compiling Smart Contracts

- Download the docker
```
docker pull eosio/eos-dev
```
- Start the blockchain
Careful about the directory you mount for work.
```
sudo docker run --rm --name eosio -d -p 8888:8888 -p 9876:9876 -v /Users/gautamanand/Library/Github/serganus/ReliefChain-smartcontracts:/tmp/work -v /tmp/eosio/data:/mnt/dev/data -v /tmp/eosio/config:/mnt/dev/config eosio/eos-dev /bin/bash -c "nodeos -e -p eosio --plugin eosio::wallet_api_plugin --plugin eosio::wallet_plugin --plugin eosio::producer_plugin --plugin eosio::history_plugin --plugin eosio::chain_api_plugin --plugin eosio::history_api_plugin --plugin eosio::http_plugin -d /mnt/dev/data --config-dir /mnt/dev/config --http-server-address=0.0.0.0:8888 --access-control-allow-origin=* --contracts-console"
```
- Check if this works
Open the web browser, to load chain info: http://localhost:8888/v1/chain/get_info
```
sudo docker logs --tail 10 eosio
```
- Start the cleos
```
alias cleos='docker exec eosio /opt/eosio/bin/cleos --wallet-url http://localhost:8888'
```
- Start eosiocpp compiler
We assume you have mapped your local contracts in /tmp/work
```
docker exec -it eosio /bin/bash
cd /tmp/work
```
- Create wast/wasm from cpp
```
eosiocpp -o contract.wast contract.cpp
```
- Create abi file from hpp
```
eosiocpp -g contract.abi contract.hpp
```




![DATA MODEL](https://github.com/serganus/ReliefChain-smartcontract/blob/master/docs/datamodel.png)

![WORKFLOW](https://github.com/serganus/ReliefChain-smartcontract/blob/master/docs/workflow.png)

![WORKFLOW](https://github.com/serganus/ReliefChain-smartcontract/blob/master/docs/actions.png)
