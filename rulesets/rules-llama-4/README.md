# Llama 4 Governance Ruleset

Protects against architectural footguns introduced by Llama 4's massive context windows and Mixture-of-Experts (MoE) routing. Llama 4 is susceptible to Context Poisoning (long-context vulnerabilities) and Privilege Escalation via Action Chaining.

## Features
- **Prevents Denial of Wallet (DoW):** Mitigates recursive loop exploits by blocking infinite chained web requests.
- **Mitigates Action Chaining:** Enforces approval for high-risk combined capabilities (e.g., reading files and immediately opening network sockets).

## Installation

```bash
ssg hub pull rules-llama-4
```