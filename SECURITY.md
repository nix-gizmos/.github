# Security policy

Several of these projects exist to contain what runs inside them; a way
around that containment is a vulnerability, and we want to hear about it.
So is anything else that lets input to one of these tools do more than it
should.

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
- **nix-oci:** an input that makes it write outside the output directory, or
  an image that contains files from none of the inputs it was given (the
  closure, a base image, extra layers or commands).
- **nix-compose:** a service definition or remote request that gets a
  container more than it declared (host mounts, privileges, ports), or
  reaches the orchestration API without the access it requires.

## Out of scope

Vulnerabilities in what these projects build on (QEMU, the Linux kernel,
microvm.nix, nixpkgs, bubblewrap, containerd, CRI-O, the agents themselves)
belong upstream.
Do tell us if one of them breaks our containment, so we can work around it.

## Supported versions

The latest release and `main`. Fixes are not backported.
