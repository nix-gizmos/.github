# Contributing

Thanks for helping. This guide applies to every repository in nix-gizmos.
A repository's own `CONTRIBUTING.md` or README adds what is specific to it,
such as how to build, test and release.

Found a vulnerability? Don't open an issue or a pull request; report it
privately as the [security policy](SECURITY.md) describes.

## Commits

**Conventional Commits.** Write subjects as `type(scope): summary`, e.g.
`feat(cri): …`, `fix(launcher): …`, `docs: …`, `test(…)`, `refactor(…)` or
`chore: …`. The release version and the release notes are generated from
these subjects, so write each one for someone reading the release page. A
breaking change gets a `!` after the type and a `BREAKING CHANGE:` footer in
its own paragraph:

```
feat(egress)!: drop the v1 config format

What changed and why.

BREAKING CHANGE: v1 configs no longer load; convert them with … first.
```

**One change per commit**, with its test and its docs. A bug fix comes with a
test that fails without it.

**Signed commits.** Every commit that reaches `main` must show as
*Verified* on GitHub. SSH signing is the shortest way to get there:

```sh
git config --global gpg.format ssh
git config --global user.signingkey ~/.ssh/id_ed25519.pub
git config --global commit.gpgsign true
```

Then add the same public key on GitHub under *Settings → SSH and GPG keys →
New SSH key*, as key type **Signing Key**. GPG works as well; see
[GitHub's guide](https://docs.github.com/en/authentication/managing-commit-signature-verification).
`git log --show-signature` shows whether a commit is signed.

Already pushed unsigned commits? Sign them again where they are, without moving
the branch, then force-push it. Here `upstream` is the nix-gizmos repository:

```sh
git rebase --exec 'git commit --amend --no-edit --no-verify -S' \
  "$(git merge-base HEAD upstream/main)"
git push --force-with-lease
```

## Pull requests

- CI must pass. A first-time contributor's workflows wait until a maintainer
  approves the run.
- A maintainer requests a [CodeRabbit](https://coderabbit.ai) review, and
  every review thread has to be resolved before merging. Reply on a thread
  when you've addressed it, or explain why it doesn't apply. The bot re-checks
  and resolves it, or a maintainer does.
- If your change alters what a user sees, update the docs in the same pull
  request. Settings and environment variables are documented in the
  repository's README.
- Changes to workflows pin each action by commit SHA with a version comment
  (`uses: owner/action@<sha> # v1.2.3`) and name an explicit runner label,
  not `ubuntu-latest`. Renovate keeps both current. An action from a new
  third-party owner also has to be allowed for the organization; until it
  is, the workflow fails with `startup_failure`.

**How it gets merged.** When every commit is signed, the pull request is
merged as it is, and your commits stay in the history. When some aren't, a
maintainer may squash it into one commit, which GitHub signs. You stay its
author, and the pull request keeps the individual commits.

## License

By contributing you agree that your contribution is licensed under the
license in the repository's `LICENSE` file: MIT for most repositories,
GPL-3.0 for nix-oci and nix-compose.
