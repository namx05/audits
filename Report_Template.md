# Smart Contract Audit Report
A time-boxed security review was done by **Naman Jain**, with a focus on the security aspects of the smart contracts implementation.
## Project Info

- **Name:** <Project Name>
- **Language:** <Language>
- **Code Scope:** <Scope>
- **Commit:** <Commit Hash>
- **Audit Date:** <Timeline>
- **Audit Type:** Manual Review and Static Analysis


## About the reviewer

I'm an independent smart contract security researcher, with a focus on the EVM, Solana, CosmWasm ecosystem. I do private audits and participate in audit contests. With 31+ audits accros ecosystems, I do my best to contribute to the blockchain ecosystem and its protocols by putting time and effort into security research. I also write educational [articles](https://medium.com/@namx05) to make developers more security-aware. Check my previous work [here](https://github.com/namx05/audits) or reach out on Twitter [@namx05](https://twitter.com/namx05), or Telegram [@namx05](https://t.me/namx05).

## Vulnerability Classifications

| Vulnerability Level   | Classification                                                                               |
| --------------------- | -------------------------------------------------------------------------------------------- |
| [Critical](#Critical) | Easily exploitable by anyone, causing loss/manipulation of assets or data.                   |
| [High](#High)         | Arduously exploitable by a subset of addresses, causing loss/manipulation of assets or data. |
| [Medium](#Medium)     | Inherent risk of future exploits that may or may not impact the smart contract execution.    |
| [Low](#Low)           | Minor deviation from best practices.                                                         |
| [Gas](#Gas)           | Best practices for gas optimazations.                                                       |

## Findings & Resolutions

During the review, a total of <total_issues> issues were found, out of which <_> were of High severity and <_> were Medium findings.

| ID           | Title | Severity | Status |
| ------------ | ----- | -------- | ------ |
| [C-01](#C01) |       |          |        |
| [H-01](#H01) |       |          |        |
| [M-01](#M01) |       |          |        |
| [L-01](#L01) |       |          |        |

### Critical Risk

#### Issue title

**Severity:** High

**Context:** [`Contract.sol#L160-L165`](https://github.com/actuallink)

**Description:**

**Code Snippet**

```solidity
contract Test {
    ...
    // Code blocks must be indented with 4 spaces.
}
```

**Impact:**

**Recommendation:**

```diff
+ use diff syntax to describe what should be changed
- ...
```

### High Risk

### Medium Risk

### Low Risk

### Gas Optimizations

## Disclaimer

A smart contract security review can never verify the complete absence of vulnerabilities. This is a time, resource and expertise bound effort where we try to find as many vulnerabilities as possible. We can not guarantee 100% security after the review or even if the review will find any problems with your smart contracts. Subsequent security reviews, bug bounty programs and on-chain monitoring are strongly recommended.