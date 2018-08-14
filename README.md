# QIQ Crowdsale Smart Contracts (Crowdsale and ERC20)

Contains the below three files:
1. **SafeMath.sol**. OpenZeppelin's implementation of SafeMath.
2. **QTC.sol**. QIQ token.
3. **Crowdsale.sol**. Crowdsale contract responsible for token distribution.

<br />

## Deployment Steps
1. Deploy **QTC.sol**, no additional constructor parameters needed. Use `distributeTokens()` function to execute private allocations.
2. Deploy **Crowdsale.sol**. Constructor parameters:
   - (address) `_QIQToken` : address of deployed QIQ token
   - (address) `_contributionColdStorage`  : address of cold storage to hold contribution amount
   - (uint256) `_hardCap`  : Hard cap. Affects `isCrowdSaleOngoing()`
   - (uint256) `_startDate`  : Start date for the contract to receive contribution in UNIX time. Affects `isCrowdSaleOngoing()`
   - (uint256) `_endDate`  : End date which closes the contract from receiving contribution in UNIX time. Affects `isCrowdSaleOngoing()`
3. Assign Crowdsale address to QIQ token contract under `setDistributionAddress()`.
4. Whitelist participants with `addToWhiteList()`.
5. Allocate QIQ tokens to Crowdsale contract address for distribution management. Likewise, use `distributeTokens()`.
6. Complete token sales. Burn remainder tokens with `burnTokens()`.

<br />

## Edge Cases:
1. Call `withdrawTokens()` with amount as input parameter if tokens need to be withdrawn. Callable by owner only.
2. Call `emergencyERC20Drain()` if other tokens are accidentally sent to this contract address. Callable by owner only.
3. Call `haltTokenSales()` with _TRUE_ as input parameter if an emergency occurs. This will shut down the contract. Callable by owner only.

<br />

## Post Token Sales
1. Call `enableTransfers()` on QIQ token contract.
