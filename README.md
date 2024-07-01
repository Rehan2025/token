# MyToken Contract

This Solidity contract implements a simple ERC-20-like token with minting and burning functionalities.

## Features

- **Public Variables**: 
  - `name`: The name of the token.
  - `symbol`: The abbreviation of the token.
  - `totalSupply`: The total supply of the token.

- **Mapping**:
  - `balances`: A mapping from addresses to their respective token balances.

- **Functions**:
  - `mint(address _to, uint256 _amount)`: Mints new tokens, increasing the total supply and the balance of the specified address.
  - `burn(address _from, uint256 _amount)`: Burns tokens, decreasing the total supply and the balance of the specified address. It ensures that the address has enough tokens to burn.

- **Events**:
  - `Transfer(address indexed from, address indexed to, uint256 value)`: Logs transfer activity, including minting (from the zero address) and burning (to the zero address).

## Getting Started

These instructions will help you deploy and interact with the contract.

### Prerequisites

- [Node.js](https://nodejs.org/)
- [npm](https://www.npmjs.com/)
- [Truffle](https://www.trufflesuite.com/truffle)
- [Ganache](https://www.trufflesuite.com/ganache) (for local development)

### Installation

1. Install Truffle globally:
    ```bash
    npm install -g truffle
    ```

2. Initialize a Truffle project:
    ```bash
    mkdir MyToken
    cd MyToken
    truffle init
    ```

3. Create the contract file in `contracts/MyToken.sol` and paste the following content:

    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;

    contract MyToken {
        // Public variables to store token details
        string public name;
        string public symbol;
        uint256 public totalSupply;

        // Mapping to store balances of addresses
        mapping(address => uint256) public balances;

        // Constructor to initialize the token details
        constructor(string memory _name, string memory _symbol) {
            name = _name;
            symbol = _symbol;
            totalSupply = 0;
        }

        // Function to mint new tokens
        function mint(address _to, uint256 _amount) public {
            require(_to != address(0), "Invalid address");

            totalSupply += _amount;
            balances[_to] += _amount;

            emit Transfer(address(0), _to, _amount);
        }

        // Function to burn tokens
        function burn(address _from, uint256 _amount) public {
            require(_from != address(0), "Invalid address");
            require(balances[_from] >= _amount, "Insufficient balance");

            totalSupply -= _amount;
            balances[_from] -= _amount;

            emit Transfer(_from, address(0), _amount);
        }

        // Event to log transfer activity
        event Transfer(address indexed from, address indexed to, uint256 value);
    }
    ```

4. Compile the contract:
    ```bash
    truffle compile
    ```

5. Deploy the contract:
    - Create a migration file in `migrations/2_deploy_contracts.js`:

        ```javascript
        const MyToken = artifacts.require("MyToken");

        module.exports = function(deployer) {
            deployer.deploy(MyToken, "MyTokenName", "MTK");
        };
        ```

    - Run the migration:
        ```bash
        truffle migrate
        ```

### Interacting with the Contract

1. Start the Truffle console:
    ```bash
    truffle console
    ```

2. Get the deployed contract instance:
    ```javascript
    let instance = await MyToken.deployed();
    ```

3. Mint tokens:
    ```javascript
    await instance.mint("0xYourAddress", 1000);
    ```

4. Burn tokens:
    ```javascript
    await instance.burn("0xYourAddress", 500);
    ```

5. Check the balance of an address:
    ```javascript
    let balance = await instance.balances("0xYourAddress");
    console.log(balance.toString());
    ```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
