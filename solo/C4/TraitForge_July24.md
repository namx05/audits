# Findings

## High Risk

## Admin's incorrect `taxCut` adjustment will lead to inaccurate share distribution for `devShares` and `nukeFundContribution`

**Severity:** High

**Context:**

[NukeFund.sol#L41](https://github.com/code-423n4/2024-07-traitforge/blob/279b2887e3d38bc219a05d332cbcb0655b2dc644/contracts/NukeFund/NukeFund.sol#L41) <br>
[EntityTrading.sol#L72](https://github.com/code-423n4/2024-07-traitforge/blob/279b2887e3d38bc219a05d332cbcb0655b2dc644/contracts/EntityTrading/EntityTrading.sol#L72) <br>
[EntityForging.sol#L146](https://github.com/code-423n4/2024-07-traitforge/blob/279b2887e3d38bc219a05d332cbcb0655b2dc644/contracts/EntityForging/EntityForging.sol#L146)

### Vulnerability details

**Summary:**

The `taxCut` variable in `EntityForging.sol` is used to calculate the developer fee as `devFee = forgingFee / taxCut`, where the initial value of `taxCut` is set to `10`, implicitly assuming it represents a 10% cut. However, this assumption only holds if the `taxCut` value remains at 10. If the admin changes the `taxCut` value to another number (e.g., 25), the resulting calculation does not correspond to the intended percentage (25%). Instead, it calculates the developer fee as `forgingFee / 25`, which can lead to incorrect fee distribution towards `devShares` and `nukeFundContribution`.

This same issue also present in `EntityTrading.sol` and `NukeFund.sol` which affects the calculation of `devShares` and `nukeFundContribution`.

**Code Snippet**

<details>
<summary>NukeFund.sol</summary>

```solidity
receive() external payable {
@>  uint256 devShare = msg.value / taxCut; //@audit
    uint256 remainingFund = msg.value - devShare; // Calculate remaining funds to add to the fund
     ...
}
```

</details>

<details>
<summary>EntityTrading.sol</summary>

```solidity
function buyNFT(uint256 tokenId) external payable whenNotPaused nonReentrant {
    ...
    //transfer eth to seller (distribute to nukefund)
@>  uint256 nukeFundContribution = msg.value / taxCut; //@audit
    uint256 sellerProceeds = msg.value - nukeFundContribution;
    ...
}
```

</details>

<details>
<summary>EntityForging.sol</summary>

```solidity
    function forgeWithListed(
    uint256 forgerTokenId,
    uint256 mergerTokenId
    ) external payable whenNotPaused nonReentrant returns (uint256) {
    ...
    require(
        mergerForgePotential > 0 &&
        forgingCounts[mergerTokenId] <= mergerForgePotential,
        'forgePotential insufficient'
    );
@>  uint256 devFee = forgingFee / taxCut; //@audit
    uint256 forgerShare = forgingFee - devFee;
    ...
    }
```

</details>
<p>

**Proof of Concept:**

- Bob is a user who performs an operation with a `forgingFee` of 1000 wei.
- The contract initially has a `taxCut` value of 10, so the developer fee is calculated as 100 wei, representing a 10% fee.
- The admin decides to change the `taxCut` value to 25, intending to set a 25% fee.
- The new calculation results in a developer fee of 40 wei, representing a 4% fee instead of the intended 25%.
- This miscalculation affects the `devShares` and `nukeFundContribution` in different contracts, leading to inaccurate fee distributions.

**Recommendation:**

It is recommended to express `taxCut` as a fraction of 100 for all three instances, allowing for percentage calculations. Eg of `EntityForging.sol`

```diff
diff --git a/contracts/EntityForging/EntityForging.sol b/contracts/EntityForging/EntityForging.sol
index c9ce23b..063257d 100644
--- a/contracts/EntityForging/EntityForging.sol
+++ b/contracts/EntityForging/EntityForging.sol
@@ -143,7 +143,7 @@ contract EntityForging is IEntityForging, ReentrancyGuard, Ownable, Pausable {
     'forgePotential insufficient'
   );

-    uint256 devFee = forgingFee / taxCut;
+    uint256 devFee = (forgingFee * taxCut) / 100;
   uint256 forgerShare = forgingFee - devFee;
   address payable forgerOwner = payable(nftContract.ownerOf(forgerTokenId));
```
