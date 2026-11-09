# nix-gizmos

Small, sharp tools built on Nix.

| | |
|---|---|
| [agent-vm](https://github.com/nix-gizmos/agent-vm) | Runs AI coding agents (Claude Code, Gemini CLI, Codex, pi) in disposable NixOS microVMs on QEMU/KVM. The project directory is mounted at `/work`. Egress is sealed and goes through an allowlisting proxy with an API budget. A launch record lists what each session was allowed to do. |
| [microvm-policy](https://github.com/nix-gizmos/microvm-policy) | The containment layer agent-vm is built on, usable by any [microvm.nix](https://github.com/microvm-nix/microvm.nix) guest: the egress proxy with its audit log and budgets, the sealed-egress guest module, and the workspace write guard and ephemeral mode. |
| [microvm-audit](https://github.com/nix-gizmos/microvm-audit) | Runs a pinned security-audit skill against one commit of a repository in a sealed agent-vm VM. Target code runs in a per-process sandbox. Each run produces a report and evidence of how contained it was. |
| [nix-oci](https://github.com/nix-gizmos/nix-oci) | Writes a Nix closure as a plain, bit-for-bit reproducible OCI image layout, layered for registry dedup, without a daemon. |
| [nix-compose](https://github.com/nix-gizmos/nix-compose) | Defines services in Nix or a `nix-compose.yaml` and runs them on containerd or CRI-O, with plan, drift and rollback. |
| [flake-diff-action](https://github.com/nix-gizmos/flake-diff-action) | Says what a `flake.lock` change does to what a flake builds, from evaluation alone: which attributes change, and which package versions move. A CLI, and a Node-free action for GitHub and Forgejo that posts the report on the pull request. |

```sh
WORK_DIR=. nix run github:nix-gizmos/agent-vm
```

Builds are cached at `https://nix-gizmos.cachix.org`, with the public key
`nix-gizmos.cachix.org-1:a8qWp7lYufNBEKQEpJf54r0WVE0ksypqnFxOyemSlX4=`.

Found a vulnerability? Please report it privately; see the
[security policy](https://github.com/nix-gizmos/.github/blob/main/SECURITY.md).
