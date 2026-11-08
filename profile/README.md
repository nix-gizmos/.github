# microvm-tools

Nix tools for running coding agents in sealed microVMs.

| | |
|---|---|
| [agent-vm](https://github.com/microvm-tools/agent-vm) | Runs AI coding agents (Claude Code, Gemini CLI, Codex, pi) in disposable NixOS microVMs on QEMU/KVM. The project directory is mounted at `/work`. Egress is sealed and goes through an allowlisting proxy with an API budget. A launch record lists what each session was allowed to do. |
| [microvm-policy](https://github.com/microvm-tools/microvm-policy) | The containment layer agent-vm is built on, usable by any [microvm.nix](https://github.com/microvm-nix/microvm.nix) guest: the egress proxy with its audit log and budgets, the sealed-egress guest module, and the workspace write guard and ephemeral mode. |
| [microvm-audit](https://github.com/microvm-tools/microvm-audit) | Runs a pinned security-audit skill against one commit of a repository in a sealed agent-vm VM. Target code runs in a per-process sandbox. Each run produces a report and evidence of how contained it was. |

```sh
WORK_DIR=. nix run github:microvm-tools/agent-vm
```

Builds are cached at `https://microvm-tools.cachix.org`, with the public key
`microvm-tools.cachix.org-1:OmNkdhRACxrceImh52cuegLuzJCj5hZFwFA8scRBk7A=`.

Found a way out of the sandbox? Please report it privately; see the
[security policy](https://github.com/microvm-tools/.github/blob/main/SECURITY.md).
