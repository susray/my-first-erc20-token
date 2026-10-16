// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC20, Ownable {
    uint256 public maxSupply;

    event TokensMinted(address indexed to, uint256 amount);
    event TokensBurned(address indexed from, uint256 amount);

    constructor(
        string memory _name,
        string memory _symbol,
        uint256 _initialSupply,
        uint256 _maxSupply
    ) ERC20(_name, _symbol) Ownable(msg.sender) {
        require(_initialSupply <= _maxSupply, "Initial supply exceeds max supply");

        maxSupply = _maxSupply;
        _mint(msg.sender, _initialSupply);
    }

    function mint(address to, uint256 amount) public onlyOwner {
        require(totalSupply() + amount <= maxSupply, "Max supply reached");
        _mint(to, amount);

        emit TokensMinted(to, amount);
    }

    function burn(uint256 amount) public {
        _burn(msg.sender, amount);

        emit TokensBurned(msg.sender, amount);
    }
}# my-first-erc20-token
My First ERC-20 Token is a beginner Solidity project built with OpenZeppelin. It creates a custom ERC-20 token with minting, burning, transfers, approvals, and balance checking. The project demonstrates the ERC-20 standard, token supply, allowances, events, and smart-contract deployment using Remix IDE.
# My First ERC-20 Token

My First ERC-20 Token is a beginner-friendly Solidity project built using OpenZeppelin and Remix IDE.

## About

This project creates a custom ERC-20 token called **My First Token (MFT)**. It demonstrates how ERC-20 tokens work on Ethereum-compatible blockchains.

## Features

- ERC-20 standard implementation
- Token name, symbol, decimals, and total supply
- Transfer tokens between wallets
- Check wallet balances
- Approve another address to spend tokens
- Transfer tokens using an allowance
- Mint new tokens
- Burn tokens
- Maximum supply limit
- Ownership control for minting
- Events for minting and burning

## Technologies Used

- Solidity
- OpenZeppelin Contracts
- Remix IDE
- Ethereum Virtual Machine (EVM)
- Remix VM / MetaMask

## Contract Functions

| Function | Description |
|---|---|
| `name()` | Returns the token name |
| `symbol()` | Returns the token symbol |
| `decimals()` | Returns the number of decimals |
| `totalSupply()` | Returns the total token supply |
| `balanceOf(address)` | Returns the token balance of an address |
| `transfer(address, uint256)` | Transfers tokens to another address |
| `approve(address, uint256)` | Approves an address to spend tokens |
| `transferFrom(address, address, uint256)` | Transfers tokens using an allowance |
| `mint(address, uint256)` | Mints new tokens, only by the owner |
| `burn(uint256)` | Burns tokens from the caller’s balance |

## How to Deploy

1. Open Remix IDE.
2. Create a new file: `contracts/MyToken.sol`.
3. Paste the contract code.
4. Compile using Solidity 0.8.20 or later.
5. Go to **Deploy & Run Transactions**.
6. Select **Remix VM**.
7. Enter token details in the constructor.
8. Click **Deploy**.
9. Interact with the contract using Remix.

## Example Constructor Values

```text
_name: My First Token
_symbol: MFT
_initialSupply: 1000000
_maxSupply: 10000000
```

## What I Learned

- How the ERC-20 token standard works
- How token transfers and approvals work
- How allowances and `transferFrom` are used
- How to mint and burn tokens
- How to use OpenZeppelin contracts
- How to deploy and interact with a smart contract in Remix

## Security Notes

- Only the contract owner can mint new tokens.
- The maximum supply prevents unlimited minting.
- Burning is limited to the caller’s own token balance.
- This project is for learning purposes and has not been professionally audited.

## License

MIT
