# SigmaShake Free Subscription Ruleset (Public)

This public ruleset provides basic protection against common developer "footguns" that AI agents might accidentally trigger.

## Features
- **Prevents System Halts:** Blocks `shutdown`, `reboot`, and `halt` commands.
- **Prevents Resource Exhaustion (OOM & CPU):** Blocks known fork-bomb patterns, massive memory allocations (`dd if=/dev/zero`), and `stress` tests.
- **Prevents System Freezes:** Stops the AI from disabling critical input devices (mouse/keyboard).

## Installation

```bash
ssg hub pull rules-free-subscription
```