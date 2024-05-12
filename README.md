# gh-actions-git-crypt-action

A fork of [amplium/git-crypt-action](https://github.com/amplium/git-crypt-action/) with some enhancements as follows:
- Run `git stash` before locking the repository in `post.sh`.
- Add `-a` argument to `git lock` in `post.sh` to lock all keys.

`git-crypt-action` speeds up and simplifies using [`git-crypt`](https://github.com/AGWA/git-crypt) inside your GitHub
Action workflows by downloading a pre-built docker image and unlocking your
repository. This has the benefit of being faster than having to `apt-get
install git-crypt`. It also takes care of re-locking the repository before
finishing your workflow.

To use this workflow, export your key and encode it with `base64`, then
register it as a GitHub Secret.

```bash
❯ git-crypt export-key -- - | base64
```

Finally, use it in your workflow.

```yaml
jobs:
  some_job:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: c0x12c/gh-actions-git-crypt-action@v0.1.0
        with:
          key_encoded: ${{ secrets.KEY }}
```
