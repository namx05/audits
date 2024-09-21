# Findings

## Medium Risk

## Lack of Access Control in `setDrawManager` Function

**Severity:** Medium

**Context:** [`PrizePool.sol#L299`](https://github.com/GenerationSoftware/pt-v5-prize-pool/blob/4bc8a12b857856828c018510b5500d722b79ca3a/src/PrizePool.sol#L299)

### Vulnerability details

**Summary:**

The `setDrawManager` function lacks proper access control, allowing any address to change the `drawManager` variable. This can pose a security risk as it allows unauthorized users to modify critical system settings.

<!-- ## Code Snippet: -->

<details>
<summary> Code Snippet </summary>

```solidity
function setDrawManager(address _drawManager) external {
  if (drawManager != address(0)) {
    revert DrawManagerAlreadySet();
  }
  drawManager = _drawManager;

  emit DrawManagerSet(_drawManager);
}
```
</details>
<br>

**Impact:**

The absence of access control introduces the following potential risks:

- Any user or contract can call the `setDrawManager` function and change the drawManager address.
- The absence of access control undermines the trustworthiness of the smart contract, as it allows unauthorized individuals to tamper with crucial settings.

**Recommendation:**

To address the issue of lacking access control, it is recommended to implement proper access control mechanisms.
