# MyToken

My project is related to token creation to store details of my custom token and to manage it.

## Description

In this project of token creation first i have created a contract which will store the details of my token such as token name, token abbr. and total supply. 
I had made these variables as public. 

Second step is to create a mapping variable to track how many tokens each address holds. The keys of the mapping are Ethereum addresses.
The values are unsigned integers representing the token balance associated with each address.

Third step is to create a mint function that allows new tokens to be added to the assigned adderess. Parameters are _value and _address. Increases the totalSupply by the _value and
Increases the balance of the _to address by the _value. For simplicity this function has been made public.

Forth step is to create another function named burn function. Functionality of this function is to destroy tokens by a specific value from the given address which is opposite to 
that of mint function. functions Checks if the balance of the _from address is greater than or equal to the _value to be burned. If sufficient balance exists, it decreases the 
totalSupply by _value and decreases the balance of the _from address by _value. 
The burn function includes a crucial check to prevent errors:
Before burning tokens, it verifies that the address initiating the burn (_from) has enough tokens to cover the amount being burned. 
This prevents accidental over-burning and helps maintain the integrity of the token's supply.

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.
Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., MyToken.sol). 
Copy and paste the following code into the file:

// SPDX-License-Identifier: MIT
pragma solidity 0.8.18;
contract myToken {

    string public tokenName = "AELPH";
    string public tokenAbbrv = "ALP";
    uint public totSupply = 0; 

    mapping(address => uint) public balances;

    function mint(uint _value, address _address) public {
        totSupply += _value;
        balances[_address] += _value;
    }

    function burn(uint _value, address _address) public {
        if (balances[_address] >= _value){
            totSupply -= _value;
            balances[_address] -= _value;
        }
    }
}

## Help

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.18" 
(or another compatible version), and then click on the "Compile MyToken.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. 
Select the "Mytoken" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by calling the mint, burn function or check balance. Click on the "MyToken" 
contract in the left-hand sidebar, and then click on the "mint" or "burn" function. Finally, click on the "transact" button to execute the 
function and retrieve the token you burned or minted.

## Authors

Ronit 
