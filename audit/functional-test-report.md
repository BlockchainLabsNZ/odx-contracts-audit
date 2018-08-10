# Functional tests 
Tests are conducted on the Kovan test network. The following contracts has been verified on Etherscan. 
  
## [`ODXToken[0x334ba0]`](https://kovan.etherscan.io/address/0x334ba0dc29ad33804d39bf93661e821608e040e2#code) 
## [`ODXPrivateSale[0xe9c590]`](https://kovan.etherscan.io/address/0x67Df0f60C955f8C093A422148a6FA119e2ac7112#code) 
## [`ODXCrowdsale[0x780a56]`](https://kovan.etherscan.io/address/0x4f92d6d4424d0086742b3653c551e17bda26cee8#code) 
 
  
## Accounts 
  
* Owner: [0x006F3FCdDaf248D1a4C9A7fd62939963AAAe5a67](https://kovan.etherscan.io/address/0x006F3FCdDaf248D1a4C9A7fd62939963AAAe5a67) 
* Privatesale agent / Whitelist agent: [0x00c7e82F3E4615a50C70262b16AEDf05C7D4E211](https://kovan.etherscan.io/address/0x00c7e82F3E4615a50C70262b16AEDf05C7D4E211) 
* Investor:[0x9Feb4d6065CdAA8b7C0B76796D431af2eE01579e](https://kovan.etherscan.io/address/0x9feb4d6065cdaa8b7c0b76796d431af2ee01579e) 
  
## Expected behaviour test for customized function in ODXToken 
- [x] Only owner can set the mint agent of the token contract. [0xcac5bc](https://kovan.etherscan.io/tx/0xcac5bca808d7ed84554b905df552824a20575e4859b271280cac1953f8b54b4a) 
 
## Expected behaviour tests of ODXPrivateSale 
- [x] Non-owner cannot change the owner of the private sale contract. [0xa29102](https://kovan.etherscan.io/tx/0xa2910251790e4bd9c2900cd5f49e0bf438577ca1ef9b8a22e2f4e8875f139ecb) 
- [x] Only owner can transfer the ownership to other address. [0x645da8](https://kovan.etherscan.io/tx/0x645da83ba283e1f2efd33db9dc5889fbbd8812341e8cfb969f63ed3f45cbefa7) 
- [x] Non-owner cannot set private sale agent. [0x30dd0b](https://kovan.etherscan.io/tx/0x30dd0b3ad2f68c154d3c59b0363568bf65dd60d3fed58b33050ebb644ebfc32c) 
- [x] Owner can set private sale agent. [0x9e8b13](https://kovan.etherscan.io/tx/0x9e8b13ac204a259c29b302b7c95f5d064d2939d9e5de38fc508a2b39876e97f5) 
- [x] Owner can add an investor to private sale and set locked tokens to that address.[0xcdfab5](https://kovan.etherscan.io/tx/0xcdfab5f899194206b861edfc1d20f05a09da5fb1142aa587f2f256ab8feb56b6) 
- [x] The function `updatePrivateSaleWithMonthlyLockupByIndex()` cannot be executed if the release time is reached.[0x80c4a7](https://kovan.etherscan.io/tx/0x80c4a7ecbd44129553e5a38fd007b7da312be1de10d94636707a05e24f6e65fa) 
- [x] Locked tokens can be released to a specific investor by private sale agent entering lock time index once release time is reached.[0xda7b52](https://kovan.etherscan.io/tx/0xda7b52718928921055445162765bb38111dc460bcb3286d42c5d34726dd4089c) 
- [x] Investor can claim his tokens once time is reached.[0x228706](https://kovan.etherscan.io/tx/0x228706b5c0727e0d4f3666511e6ae7522a6201b7a2307ae145ac4fee06d21f6b) 
- [x] Locked tokens at all spans can be released to a specific investor by private sale agent. [0x84aef4](https://kovan.etherscan.io/tx/0x84aef4f85cd88c438d68311a92ebe2dea4e6f7f261b14b001155e5cc7c98a549) 
  
## Expected behaviour tests of ODXCrowdsale 
- [x] Owner can add investor into whitelist. [0x4dbf57](https://kovan.etherscan.io/tx/0x4dbf57d44e1f1627adee1a101b738fc974ffdb5ea5ccce806b3d5a4ebc625031) 
- [x] Owner can add many investors into whitelist at one time.[0xc6eda6](https://kovan.etherscan.io/tx/0xc6eda60c8e4ca5188a5609e3c63e35b73c7a9329b5daaf16bbdd744e985ea0aa) 
- [x] Non-Owner cannot transfer the ownership of the contract. [0x99bbb1](https://kovan.etherscan.io/tx/0x99bbb10a871da84b69e6bdd0ae5dd0100b2d5d799e2f77fde60fb08de1972de2) 
- [x] Owner can set whitelist agent.[0x7200fd](https://kovan.etherscan.io/tx/0x7200fd879242579066990717a5d2b58ef890c2c56adda71306840da2a4fb207d) 
- [x] Rate can be updated by the owner. [0xeea8c4](https://kovan.etherscan.io/tx/0xeea8c424e913825473e8e52c243655d21b5714157621ae43730a3807c130c2ab) 
- [x] Whitelisted investor can be removed from whitelist by whitelist agent. [0xafa2b7](https://kovan.etherscan.io/tx/0xafa2b7540ac863a03233d9d837e13aa1dc405892d70ff3a7044714d082a06653) 
- [x] Any one can buy tokens while crowdsale is open. [0xc3026a](https://kovan.etherscan.io/tx/0xc3026a268ba116aecc2f165faca76b34b4f3039665ca9c02fcfe8aab4c68b9d8)