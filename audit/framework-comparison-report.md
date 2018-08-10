## Framework used

Generally, this project is using a solidity framework [openzeppelin-solidity](https://github.com/OpenZeppelin/openzeppelin-solidity). Various commits of versions are used and re-organized. However, that doesn't break the contract's behaviour. <br>
After comparison with commit[9fd61177](https://github.com/OpenZeppelin/openzeppelin-solidity/tree/9fd61177c3046e85fe3a492dd885322da20cc05f), 8/20 of all contracts are fully self-developed. 8/20 of the contracts stay the same features with the framework. See details from the [list](https://gist.github.com/ryu9827/4b702b2a85dcb0cca1c17c668bd73c50). And 4/20 have some changes from the framework.<br>

The contracts having big modifications from original framework are listed below:

* TimedCrowdsale.sol
A internal function `_preValidatePurchase()` is removed.
```
  /**
   * @dev Extend parent behavior requiring to be within contributing period
   * @param _beneficiary Token purchaser
   * @param _weiAmount Amount of wei contributed
   */
  function _preValidatePurchase(
    address _beneficiary,
    uint256 _weiAmount
  )
    internal
    onlyWhileOpen
  {
    super._preValidatePurchase(_beneficiary, _weiAmount);
  }

}
```

* Crowdsale.sol
A `uint` variable `tokensToBeMinted` is introduced for updating the token amount need to be minted.
```
...
  // Amount of tokens to be minted
  uint256 public tokensToBeMinted;
...

  //Line 87, new added tokensToBeMinted is used here
    //updated token count to be minted
    tokensToBeMinted = tokensToBeMinted.add(tokens);

...
  //Line 93, event is renamed to AllocateTokens and used here
    emit AllocateTokens(
      msg.sender,
      _beneficiary,
      weiAmount,
      tokens
    );
...
```

Two internal functions `_postValidatePurchase` and `_updatePurchasingState` are commented out from the code, both of them are optional functions. Their usage is commented out as well.
```
...
  //Line 100 - 103
    //_updatePurchasingState(_beneficiary, weiAmount);

    _forwardFunds();
    //_postValidatePurchase(_beneficiary, weiAmount);
...
  //Line 126 - 128
  //function _postValidatePurchase(address _beneficiary, uint256 _weiAmount) internal {
    // optional override
  //}
...
  //Line 153 - 155
    //function _updatePurchasingState(address _beneficiary, uint256 _weiAmount) internal {
    // optional override
  //}
...
```

* CappedCrowdsale.sol
A new `uint` variable `tokenCap` and function `tokenCapReached()` are introduced to the contract for checking whether the token cap has been reached.
```
...
//Line 16
  uint256 public tokenCap;
...
//Line 42 -43
  function tokenCapReached() public view returns (bool) {
    return tokensToBeMinted >= tokenCap;
```

* CappedMintableToken.sol
This contract is a mixin of `MintableToken.sol` and `CappedToken.sol` and renamed to current name. A mapping `mintAgents` is added for storing mint agent address(crowdsale contract address), which has permission of minting tokens. <br>
Modifier `hasMintPermission` is replaced by `onlyMintAgent` through out the contract.
```
...
//Line 13
  event MintingAgentChanged(address addr, bool state);
...
//Line 18
  mapping (address => bool) public mintAgents;
...
//Line 25 - 31
  modifier onlyMintAgent() {
    // crowdsale contracts or owner are allowed to mint new tokens
    if(!mintAgents[msg.sender] && (msg.sender != owner)) {
        revert();
    }
    _;
  }
...
//Line 40 - 46
  /**
   * Owner can allow a crowdsale contract to mint new tokens.
   */
  function setMintAgent(address addr, bool state) onlyOwner canMint public {
    mintAgents[addr] = state;
    emit MintingAgentChanged(addr, state);
  }
...
//Line 54 - 55
  function mint(address _to, uint256 _amount) onlyMintAgent canMint public returns (bool) {
    require(totalSupply_.add(_amount) <= cap);
...
```

* WhitelistedCrowdsale.sol
This contract has the same name with the one in openzeppelin, but they are hugely different. We consider it a self-developed contract and performed a full analysis on it in detail.
