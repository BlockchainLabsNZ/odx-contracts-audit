# ODX Smart Contract Audit Report
<br>

## Preamble
This audit report was undertaken by <b>BlockchainLabs.nz</b> for the purpose of providing feedback to <b>Zipper</b>. <br>It has subsequently been shared publicly without any express or implied warranty.

Solidity contracts were sourced from the public Github repos [odxnetwork/smartconracts-token/](https://github.com/odxnetwork/smartconracts-token/tree/1af271d30db56b913b5c88df21920275259ab057) and [odxnetwork/crowdsale](https://github.com/odxnetwork/smartcontracts-crowdsale/tree/1ee8304974981ad701f6f1e901c8cc9691734808) - we would encourage all community members and token holders to make their own assessment of the contracts.

<br>

## Scope
The following contract was a subject for static, dynamic and functional analyses:

Contracts
  - [BasicToken.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/BasicToken.sol)
  - [ERC20.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/ERC20.sol)
  - [ODXPrivateSale.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/ODXPrivateSale.sol)
  - [StandardToken.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/StandardToken.sol)
  - [BurnableToken.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/BurnableToken.sol)
  - [ERC20Basic.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/ERC20Basic.sol)
  - [ODXToken.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/ODXToken.sol)
  - [TimedCrowdsale.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/TimedCrowdsale.sol)
  - [CappedCrowdsale.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/CappedCrowdsale.sol)
  - [Ownable.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/Ownable.sol)
  - [WhitelistedCrowdsale.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/WhitelistedCrowdsale.sol)
  - [CappedMintableToken.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/CappedMintableToken.sol)
  - [MockODXCrowdsale.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/MockODXCrowdsale.sol)
  - [PrivateSaleRules.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/PrivateSaleRules.sol)
  - [Crowdsale.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/Crowdsale.sol)
  - [MockODXPrivateSale.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/MockODXPrivateSale.sol)
  - [SafeMath.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/SafeMath.sol)
  - [CrowdsaleNewRules.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/CrowdsaleNewRules.sol)
  - [ODXCrowdsale.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/ODXCrowdsale.sol)
  - [StandardBurnableToken.sol](https://github.com/BlockchainLabsNZ/odx-contracts-audit/blob/audit/contracts/StandardBurnableToken.sol)
<br>

## Focus areas
The audit report is focused on the following key areas - though this is not an exhaustive list.


### Correctness
- No correctness defects uncovered during static analysis?
- No implemented contract violations uncovered during execution?
- No other generic incorrect behaviour detected during execution?
- Adherence to adopted standards such as ERC20?

### Testability
- Test coverage across all functions and events?
- Test cases for both expected behaviour and failure modes?
- Settings for easy testing of a range of parameters?
- No reliance on nested callback functions or console logs?
- Avoidance of test scenarios calling other test scenarios?

### Security
- No presence of known security weaknesses?
- No funds at risk of malicious attempts to withdraw/transfer?
- No funds at risk of control fraud?
- Prevention of Integer Overflow or Underflow?

### Best Practice
- Explicit labeling for the visibility of functions and state variables?
- Proper management of gas limits and nested execution?
- Latest version of the Solidity compiler?

<br>

## Analysis

- [Dynamic analysis](dynamic-analysis.md)
- [Test coverage](test-coverage.md)
- [Framework Comparison](framework-comparison-report.md)
- [Functional test](functional-test-report.md)

<br>

## Issues

### Severity Description
<table>
<tr>
  <td>Minor</td>
  <td>A defect that does not have a material impact on the contract execution and is likely to be subjective.</td>
</tr>
<tr>
  <td>Moderate</td>
  <td>A defect that could impact the desired outcome of the contract execution in a specific scenario.</td>
</tr>
<tr>
  <td>Major</td>
  <td> A defect that impacts the desired outcome of the contract execution or introduces a weakness that may be exploited.</td>
</tr>
<tr>
  <td>Critical</td>
  <td>A defect that presents a significant security vulnerability or failure of the contract across a range of scenarios.</td>
</tr>
</table>

### Minor
- **Unnecessary variable assigning** - `Gas optimization` [#L147-L148](https://github.com/odxnetwork/smartcontracts-crowdsale/blob/1ee8304974981ad701f6f1e901c8cc9691734808/contracts/PrivateSaleRules.sol#L147-L148]) `uint tokenLen = _atokenAmount.length;` is unnecessary. Line 148 is the only place you use `tokenLen` and it can be changed to `require(_atokenAmount.length== lockupTimes.length);` The same thing happens again in line 189 - 191  [View on GitHub](https://github.com/BlockchainLabsNZ/odx-contracts-audit/issues/6)
- **A internal function is declared but never used** - `Best practice` [#L170](https://github.com/odxnetwork/smartcontracts-crowdsale/blob/1ee8304974981ad701f6f1e901c8cc9691734808/contracts/PrivateSaleRules.sol#L170]) Function `getTotalTokensPerArray()` is an internal function. It is declared but never used in any contracts.  [View on GitHub](https://github.com/BlockchainLabsNZ/odx-contracts-audit/issues/5)
- **Code can be simplified** - `Best practice` [#L33-L39](https://github.com/odxnetwork/smartcontracts-crowdsale/blob/1ee8304974981ad701f6f1e901c8cc9691734808/contracts/PrivateSaleRules.sol#L33-L39]) The if-revert statement can be simplified by using `require()`.  [View on GitHub](https://github.com/BlockchainLabsNZ/odx-contracts-audit/issues/4)
- **Dead code(PrivateSaleRules.sol, CrowdsaleNewRules.sol)** - `Best practice` [#L69](https://github.com/odxnetwork/smartcontracts-crowdsale/blob/1ee8304974981ad701f6f1e901c8cc9691734808/contracts/PrivateSaleRules.sol#L69]) [#L153](https://github.com/odxnetwork/smartcontracts-crowdsale/blob/1ee8304974981ad701f6f1e901c8cc9691734808/contracts/PrivateSaleRules.sol#L153]) [#L98](https://github.com/odxnetwork/smartcontracts-crowdsale/blob/1ee8304974981ad701f6f1e901c8cc9691734808/contracts/CrowdsaleNewRules.sol#L98]) Dead code should be removed.  [View on GitHub](https://github.com/BlockchainLabsNZ/odx-contracts-audit/issues/3)
- **@dev should describe function's feature.** - `Correctness` [#L43](https://github.com/odxnetwork/smartcontracts-crowdsale/blob/1ee8304974981ad701f6f1e901c8cc9691734808/contracts/PrivateSaleRules.sol#L43]) @dev says the constructor 'sets goal, additionalTokenMultiplier and minContribution' but none of them are set. It simply initializes the variable `lockupTime` and token contract address.  [View on GitHub](https://github.com/BlockchainLabsNZ/odx-contracts-audit/issues/2)
- **Prefer explicit declaration of variable types** - `Best practice` [#L29](https://github.com/odxnetwork/smartcontracts-crowdsale/blob/1ee8304974981ad701f6f1e901c8cc9691734808/contracts/PrivateSaleRules.sol#L29]) The variable type of `lockedTimeIndex` should be `uint256`. It is recommended to explicitly define your variable types and keep consistency. This confirms your intent and safeguards against a future when the default type changes. Same issue in line 93 [#L93](https://github.com/odxnetwork/smartcontracts-crowdsale/blob/1ee8304974981ad701f6f1e901c8cc9691734808/contracts/PrivateSaleRules.sol#L93]) ... [View on GitHub](https://github.com/BlockchainLabsNZ/odx-contracts-audit/issues/1)

### Moderate
- None found

### Major
- None found

### Critical
- None found


<br>

## Observations
- In `PrivateSaleRules.sol` there are two functions `releaseLockedTokens()` and `releaseLockedTokensByIndex()` which can only be called by the owner. These could be made public so that anyone could release tokens for other investors. This could potentially save the owner in gas costs, but it is a very minor tweak.
- `ODXPrivateSale` shows the lockup times as 10 minutes, 15 minutes, and 20 minutes. These seem to short to be the real production values. Is this test code that needs to be updated before deployment?

<br>

## Conclusion

The developers demonstrated an understanding of Solidity and smart contract development. We took part in carefully reviewing all source code provided, including static, dynamic, and functional testing methodology.

Overall we consider the resulting contracts following the audit feedback period adequate and have not identified any potential vulnerabilities. This contract has a low level risk of ETH and ODX being hacked or stolen from the inspected contracts.


<hr>

### Disclaimer

Our team uses our current understanding of the best practises for Solidity and Smart Contracts. Development in Solidity and for Blockchain is an emerging area of software engineering which still has a lot of room to grow, hence our current understanding of best practise may not find all of the issues in this code and design.

We have not analysed any of the assembly code generated by the Solidity compiler. We have not verified the deployment process and configurations of the contracts. We have only analysed the code outlined in the scope. We have not verified any of the claims made by any of the organisations behind this code.

Security audits do not warrant bug-free code. We encourge all users interacting with smart contract code to continue to analyse and inform themselves of any risks before interacting with any smart contracts.

