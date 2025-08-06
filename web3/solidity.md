# Solidity

### Function comparison

| Видимость  | Вызов из транзакции | Вызов из др. контракта | Вызов из своего контракта | Вызов из наследника | Gas (внутр.) | Gas (внешн.) | Примеры применения                      |
| ---------- | ------------------- | ---------------------- | ------------------------- | ------------------- | ------------ | ------------ | --------------------------------------- |
| `public`   | ✔                   | ✔                      | ✔                         | ✔                   | низкий       | высокий      | API-функции, геттеры                    |
| `external` | ✔                   | ✔                      | через `this.`             | через `this.`       | —            | высокий      | Внешний интерфейс, большие calldata     |
| `internal` | ✘                   | ✘                      | ✔                         | ✔                   | очень низкий | —            | Вспомогательные, унаследованные функции |
| `private`  | ✘                   | ✘                      | ✔                         | ✘                   | очень низкий | —            | Локальные вспомогательные функции       |



Interaction with the contract

```python
from web3 import Web3
import os

# Конфиг (рпц, приватный ключ от нашего EOA, адрес нашего EOA, адрес контракта )
INFURA_URL    = os.getenv('INFURA_URL')
PRIVATE_KEY   = os.getenv('PRIVATE_KEY')
FROM_ADDRESS  = Web3.to_checksum_address(os.getenv('FROM_ADDRESS'))
CONTRACT_ADDR = Web3.to_checksum_address(os.getenv('CONTRACT_ADDRESS'))

# Описание методов контракта
ABI = [
    {
        "inputs": [],
        "name": "lol",
        "outputs": [],
        "stateMutability": "nonpayable",
        "type": "function"
    }
]

#Подключаемся и создаем объект контракта
w3 = Web3(Web3.HTTPProvider(INFURA_URL))
if not w3.is_connected():
    raise ConnectionError("Failed to connect to ethereum node")

contract = w3.eth.contract(address=CONTRACT_ADDR, abi=ABI)


def someFunc():
    #Берем nonce для нашей транзакции
    nonce = w3.eth.get_transaction_count(FROM_ADDRESS)
    
    # Составляем саму транзакцию, вызываем функцию lol у контракта
    tx = contract.functions.lol().build_transaction({
        'from': FROM_ADDRESS,
        # Тут например могли передать value с переводом ethereum в wei
        #'value': w3.to_wei(amount_eth, 'ether'),
        'nonce': nonce,
        # Выставляем сколько готовы платить за газ
        'gas': 200000,
        'gasPrice': w3.to_wei('50', 'gwei')
    })
    
    # Подписываем и отправляем транзакцию
    signed_tx = w3.eth.account.sign_transaction(tx, PRIVATE_KEY)
    tx_hash = w3.eth.send_raw_transaction(signed_tx.raw_transaction)
    print(f"Tx sent: {tx_hash.hex()}")
    receipt = w3.eth.wait_for_transaction_receipt(tx_hash)
    print(f"Mined in block {receipt.blockNumber}")
    
if __name__ == "__main__":
    someFunc()
```
