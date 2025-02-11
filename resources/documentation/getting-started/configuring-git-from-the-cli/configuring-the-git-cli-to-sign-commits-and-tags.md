#### Configuring the Git CLI to Sign Commits and Tags

Now that you have your GPG subkey for signing commits and tags, you will need to tell the git CLI to sign commits and tags, and use your subkey to do so.

To begin, run the following to tell the git CLI to use the default `openpgp` format when signing commits and tags:

```shell
> user@workstation ~/ $ git config --global --unset gpg.format
```

You will need the ID of the subkey that you just created in order to add your identity to the git CLI, run the following to list your available keys:

```shell
> user@workstation ~/ $ gpg -K --keyid-format=long
...
------------------------------------
sec   ed25519/3AA5C34371567BD2 2025-02-06 [SC]
uid                          username (authentication and signing keyring for GitHub) <verified-github-email@example.com>
ssb   cv25519/4BB6D45482678BE3 2025-02-06 [E]
ssb   cv25519/5269150E95DAC3EB 2025-02-06 [S]
```

To set your GPG signing key in the git CLI, run the following:

```shell
> user@workstation ~/ $ git config --global user.signingkey 5269150E95DAC3EB
```

Lastly, we will tell the git CLI to sign all commits and tags by default, by running the following:

*this can be done on a per commit basis by running the `git commit` command with the `-S` flag*

```shell
> user@workstation ~/ $ git config --global commit.gpgsign true
> user@workstation ~/ $ git config --global tag.gpgSign true
```

<div>
  <a href="generating-a-gpg-subkey-for-signing-commits-and-tags.md">Previous</a>
  <a href="adding-your-gpg-signing-key-to-github.md">Next</a>
</div>