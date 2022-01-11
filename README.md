# JOET-ERC20Token

# Research on Security tokens on Ethereum

- When bitcoin was born, cryptocurrency was only considered as digital currency.
- The rise of **initial coin offerings(ICOs)** have made the term cryptocurrency a bit outdated.
- The ICO generated coins are commonly referred to as **token**.

## What is security tokens?

- Security tokens / Equity tokens is a one special kind of cryptocurrecy.
- They are essencially digital, liquid contracts for fractions of asset that already has value, like real estate, a car, corporate stoke.
- security token projects will use **smart contracts** which will automate service provider functions through software. This will replace middlemen such as lawyers,financial institutions, and so no.
- Using security tokens means investors can expect that their ownership stake is preserved on the **blockchain ledger**.
- With their ability to demonstrate value, security tokens could roil traditional financial markets in favor of the newer, more hybrid blockchain models.
- It’s inevitable that security tokens will transform equity just as bitcoin has transformed currency, because they afford the owner a direct, liquid economic interest and the expedited delivery of proceeds. Every type of ownership can be tokenized, which is a massive multi-trillion dollar addressable market.

## How security token can be implemented in a smart contract ?

### What are ERC-20?

- **Fungible Tokens**
  - Indistinguishable
- ERC20 are tokens that are deployed on a chain using what's called the erc20 token standard. it is a smart contract that actually represent a token.
- Governance token
- Secure an underlying network
- create a synthetic asset

```
>> brownie init
>> brownie complie
// will run in local network(Ganache-cli)
>> brownie run scripts/1_deploy_token.py
// will use Testnet like kovan
>> brownie run scripts/1_deploy_token.py --network kovan
```

- Create a file contracts/SecurityTokens.sol :

```c
// creating ERC20
// contracts/SecurityToken.sol
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract SecurityTokens is ERC20 {
    // wei
    constructor(uint256 initialSupply) public ERC20("JoeToken", "JoeT") {
        _mint(msg.sender, initialSupply);
    }
}

```

- Create a scripts/1_deploy_token.py :

```py
from brownie import OurToken
from scripts.helpful_scripts import get_account
from web3 import Web3

initial_supply = Web3.toWei(1000, "ether")


def main():
    account = get_account()
    our_token = OurToken.deploy(initial_supply, {"from": account}, publish_source=True)
```

- In .env file :

```
PRIVATE_KEY
WEB3_INFURA_PROJECT_ID
ETHERSCAN_TOKEN
```

- In brownie-config.yml file:

```yml
dependencies:
  - OpenZeppelin/openzeppelin-contracts@4.2.0
compiler:
  solc:
    remappings:
      - "@openzeppelin=OpenZeppelin/openzeppelin-contracts@4.2.0"
dotenv: .env
wallets:
  from_key: ${PRIVATE_KEY}
```

Created Token can be see here:[https://kovan.etherscan.io/address/0x3d6d51628585d60cf6c7b2b840e25e484ab543b5]
