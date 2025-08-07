# Ganache

### deploy block chain

_docker-compose.yml:_

```yaml
version: '3'
services:
  ganache:
    image: trufflesuite/ganache
    command: -m "12 word seed phrase" --wallet.totalAccounts=2 --miner.blockTime=1
    ports:
      - "8545:8545"
```
