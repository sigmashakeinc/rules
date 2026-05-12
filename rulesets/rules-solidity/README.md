# rules-solidity

Solidity/EVM smart contract security governance rules for AI coding agents. Enforces the most critical smart contract security patterns: blocks tx.origin authentication (phishing), selfdestruct, delegatecall to user-supplied addresses, unchecked send/transfer return values, reentrancy-vulnerable patterns, hardcoded addresses, and pre-0.8 integer overflow without SafeMath.

**7 rules · 1 file**

![rules-solidity — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-solidity)

## Install

```bash
ssg hub pull rules-solidity
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### solidity_write_safety.rules — Security (7 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-tx-origin-auth` | DENY | error | Blocks `tx.origin` auth — use `msg.sender` |
| `no-selfdestruct` | ASK | error | Flags `selfdestruct()` — irreversible |
| `no-delegatecall-user-input` | DENY | error | Blocks delegatecall to user-supplied addresses |
| `no-unchecked-send-transfer` | ASK | error | Flags unchecked `.send()`/`.call{value:}` |
| `no-reentrancy-pattern` | ASK | error | Flags external calls without nonReentrant |
| `no-hardcoded-eth-address` | ASK | warning | Flags hardcoded Ethereum addresses |
| `no-integer-overflow-unchecked` | ASK | error | Flags Solidity <0.8 without SafeMath |

## Compatible with

- Solidity 0.6+, 0.8+
- OpenZeppelin Contracts, Hardhat, Foundry
- Works alongside Slither and Mythril

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
