# SigmaShake Rules: Claude Mythos
  
  Advanced security hardening rules specifically designed to protect against sophisticated AI agent capabilities like those exhibited by Claude Mythos models.
  
  ## Included Rules
  
  - **Sensitive Paths (`00-sensitive-paths.rules`)**:
    Protects `/proc`, `.ssh`, `.git/config`, and restricts diagnostic tool usage.
    
  - **Anti-Concealment (`01-anti-concealment.rules`)**:
    Blocks git history rewriting and prevents tampering with governance components.
    
  - **Network Egress (`02-network-egress.rules`)**:
    Blocks outbound transfers to pastebins and warns on unauthorized `curl` or `netcat` usage.
    
  - **Destructive Ops HITL (`03-destructive-ops-hitl.rules`)**:
    Requires human-in-the-loop (ASK) for high impact operations such as data deletion (`drop table`, disk wiping, recursive permission changes).

  - **Custom Exploit Compilation (`04-custom-exploit-compilation.rules`)**:
    Detects and flags on-the-fly compilation of C/C++ code containing kernel headers or outputting to temporary directories.

  - **LotL Abuse (`05-lotl-abuse.rules`)**:
    Blocks Living off the Land abuse, PTY shell-spawning, and obfuscated pipeline execution.

  - **Kernel and Injection (`06-kernel-and-injection.rules`)**:
    Strictly bans kernel module manipulation (`insmod`), process injection (`LD_PRELOAD`), and kernel memory layout scans.

  - **Advanced Memory Threats (`07-advanced-memory-threats.rules`)**:
    Defends against advanced memory exploitation including KASLR defeats, SLUB allocator spraying via message queues, credential smashing, JIT spraying, and unsafe FFI primitives.

  - **Advanced Network Threats (`08-advanced-network-threats.rules`)**:
    Defends against advanced network protocol abuse, such as FreeBSD RPC chunking, out-of-band AF_UNIX sockets, and anomalous ipset bitmap bounds configurations.
