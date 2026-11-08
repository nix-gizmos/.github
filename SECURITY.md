# Security policy

These projects exist to contain what runs inside them. A way around that
containment is a vulnerability, and we want to hear about it.

## Reporting

Report privately through GitHub: open the repository's **Security** tab and
choose **Report a vulnerability**. Please don't open a public issue or pull
request for a vulnerability.

Include what you ran, what you expected the containment to stop, and what got
through. A reproduction against the latest release or `main` helps most.

## In scope

- **agent-vm:** anything a guest can reach that the launcher did not grant it,
  such as host files outside the shares, the network past the egress proxy,
  or the host's credentials. Also launch records that misstate what a
  session could do.
- **microvm-policy:** traffic the egress proxy lets through despite the
  allowlist, budgets that can be exceeded, audit-log entries that can be
  suppressed or forged, and writes the workspace guard or ephemeral mode
  fails to stop.
- **microvm-audit:** target code that escapes `audit-sandbox`, a target
  repository whose Claude configuration takes effect, and evidence that
  reports `valid` for a run that was not contained.

## Out of scope

Vulnerabilities in what these projects build on (QEMU, the Linux kernel,
microvm.nix, nixpkgs, bubblewrap, the agents themselves) belong upstream.
Do tell us if one of them breaks our containment, so we can work around it.

## Supported versions

The latest release and `main`. Fixes are not backported.
