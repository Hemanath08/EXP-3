# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:
The manufacturer records product creation details on-chain.


The product moves through different supply chain checkpoints.


The ownership of the product can be transferred securely.


Buyers can verify the product’s authenticity.


# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LuxurySupplyChain {
    struct Product {
        string name;
        address currentOwner;
        bool verified;
    }

    mapping(uint256 => Product) public products;

    event ProductRegistered(uint256 productId, string name);
    event OwnershipTransferred(uint256 productId, address newOwner);

    function registerProduct(uint256 productId, string memory name) public {
        require(products[productId].currentOwner == address(0), "Product already registered");
        products[productId] = Product(name, msg.sender, true);
        emit ProductRegistered(productId, name);
    }

    function transferOwnership(uint256 productId, address newOwner) public {
        require(products[productId].currentOwner == msg.sender, "Not the owner");
        products[productId].currentOwner = newOwner;
        emit OwnershipTransferred(productId, newOwner);
    }

    function verifyProduct(uint256 productId) public view returns (string memory, address, bool) {
        Product memory p = products[productId];
        return (p.name, p.currentOwner, p.verified);
    }
}
```
# Expected Output:
A luxury good (e.g., a Rolex watch) is registered on-chain.

<img width="1919" height="921" alt="image" src="https://github.com/user-attachments/assets/87bc09be-94a3-4fc3-9a65-236dcb7926a7" />


Ownership is transferred at every checkpoint.

<img width="1919" height="914" alt="image" src="https://github.com/user-attachments/assets/5dd28df9-5753-4fd7-89ce-20cdc12f5b05" />

Buyers can check the authenticity before purchasing.


<img width="1919" height="911" alt="image" src="https://github.com/user-attachments/assets/eb4629d9-5bc5-43b2-b8a5-023afc748e88" />

<img width="1914" height="911" alt="image" src="https://github.com/user-attachments/assets/0698675e-ef07-49e1-be90-576878093ba8" />


# High-Level Overview:
Helps prevent counterfeit luxury goods.


Teaches real-world supply chain use cases.

# RESULT : 

