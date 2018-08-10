# Dynamic Analysis

```
  Contract: ODXToken Contract
    1) Contract deployment
    total supply
      ✓ initial token supply must be zero (43ms)
    balanceOf
      when the requested account has no tokens
        ✓ returns zero
    owner
      ✓ returns the owner
    setMintAgent
      ✓ should allow when the sender is the token owner (86ms)
      ✓ should reject if sender is not the token owner (39ms)
    mint
      when the sender is mintAgent
        when the token was not finished
          ✓ should mint the requested amount (88ms)
          ✓ should emit a mint finished event (60ms)
        should reject if the token minting is finished
          ✓ reverts (77ms)
      when the sender is not a mintAgent
        ✓ should reject minting request (104ms)
    transfer
      ✓ should allow if user has sufficient balance (138ms)
      ✓ should reject if user has insufficient balance (93ms)
      ✓ should reject if transferring to an invalid address (84ms)
      ✓ should log token transfer (103ms)
    transferFrom
      when the recipient is not the zero address
        when the spender has enough approved balance
          when the owner has enough balance
            ✓ should allow transfer and decrease the spender allowance (94ms)
            ✓ should emit a transfer event (46ms)
          when the owner does not have enough balance
            ✓ reverts
        when the spender does not have enough approved balance
          when the owner has enough balance
            ✓ reverts (39ms)
          when the owner does not have enough balance
            ✓ reverts
      when the recipient is the zero address
        ✓ reverts
    transferOwnership
      ✓ when the sender is the token owner (68ms)
      ✓ should prevent non-owners from transfering
      ✓ should guard ownership against stuck state
    burn
      ✓ should allow if user has sufficient token (118ms)
      ✓ should reject if user has insufficient token (87ms)
    burnFrom
      Sufficient tokens
        Caller is not allowed to burn
          ✓ reverts (108ms)
        Caller is allowed to burn
          ✓ should allow burning and decreases token balance and total supply (235ms)
      Insufficient tokens
        Caller is not allowed to burn
          ✓ reverts (77ms)
        Caller is allowed to burn
          ✓ reverts (114ms)

  Contract: MockODXCrowdsale
    crowdsale is active
      contribution
        sender is whitelisted
          ✓ should accept contribution equal or more than minimum (51ms)
          ✓ should reject contribution less than minimum
          ✓ 1 ETH should be equivalent to 50000 ODX tokens (57ms)
          ✓ should forward funds to wallet (374ms)
          ✓ should assign tokens to sender (76ms)
          ✓ should log token allocation (65ms)
        sender is not whitelisted
          ✓ should reject any contribution : equal or more than minimum
          ✓ should reject any contribution :  less than minimum (40ms)
          ✓ should reject payments to addresses removed from whitelist (66ms)
      whitelisting
        ✓ should only allow owner to set WhitelistAgent (73ms)
        ✓ should only allow WhitelistAgents/owner to whitelist an investor (143ms)
        ✓ should correctly report whitelisted addresses (40ms)
      update rate
        ✓ should reject request if sender is not the owner
        ✓ should successfully change rate if sender is the owner (47ms)
      token delivery
        ✓ should not immediately assign tokens to beneficiary (84ms)
        ✓ should not allow beneficiaries to withdraw tokens before crowdsale ends (90ms)
    crowdsale is not active
      contribution
        ✓ should reject any contribution if crowdsale is not active (107ms)
      token delivery
        ✓ should allow whitelisted beneficiaries to withdraw tokens after crowdsale if goal is reached (193ms)
        ✓ should not allow whitelisted beneficiaries to withdraw tokens after crowdsale if goal is not reached (135ms)
        ✓ should log token distribution (172ms)
    transferOwnership
      ✓ should only allow owner to transfer ownership (95ms)
      ✓ should guard ownership against stuck state (42ms)

  Contract: MockODXPrivatesale
    setPrivateSaleAgent
      ✓ should only allow owner to set privatesaleAgent (127ms)
    addPrivateSaleWithMonthlyLockup
      ✓ should only allow privatesaleAgent/owner to call updatePrivateSaleWithMonthlyLockup (444ms)
      ✓ should reject investor has extisting privatesale contribution must use updatePrivateSaleWithMonthlyLockupByIndex (94ms)
      ✓ should reject if contribution is <= 0
      ✓ should reject if investor is not valid  (111ms)
      ✓ should reject if tokens are incomplete (116ms)
      ✓ should log update locked tokens (81ms)
    updatePrivateSaleWithMonthlyLockupByIndex
      ✓ should only allow privatesaleAgent to call updatePrivateSaleWithMonthlyLockupByIndex (94ms)
      ✓ should change token amount of the lockupindex (167ms)
      ✓ should reject if contribution is <= 0  (78ms)
      ✓ should reject if lockupIndex is not within lockeduptimes length  (92ms)
      ✓ should reject if investor has no existing contribution  (84ms)
      ✓ should reject if lockuptime of index is greater than current date  (203ms)
      ✓ should log update locked tokens (128ms)
    token distribution/release
      ✓ should not allow investor to claim tokens before lockup time (144ms)
      ✓ should allow investor to claim locked tokens past lockup time (838ms)
      ✓ should allow owner to release locked tokens past lockup time (914ms)
      ✓ should allow owner to release locked tokens past lockup time by index (738ms)
    transferOwnership
      ✓ should only allow owner to transfer ownership (102ms)
      ✓ should guard ownership against stuck state (155ms)


  70 passing (26s)
```
