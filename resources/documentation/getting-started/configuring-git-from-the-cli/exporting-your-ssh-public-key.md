#### Exporting Your SSH Public Key

Now that you have generated a new GPG subkey for authentication, you need to export the SSH public key and add it to your GitHub account in order to allow GitHub to authenticate your actions.

You will need the ID of your subkey in order to extract your SSH keys, to retrieve your subkey ID, run the following:

```shell
> user@workstation ~/ $ gpg -K --keyid-format=long
...
------------------------------------
sec   ed25519/3AA5C34371567BD2 2025-02-06 [SC]
uid                          username (authentication and signing keyring for GitHub) <verified-github-email@example.com>
ssb   cv25519/4BB6D45482678BE3 2025-02-06 [E]
ssb   cv25519/5269150E95DAC3EB 2025-02-06 [S]
ssb   cv25519/84FE2A5988AB6BA1 2025-02-06 [A]
```

Your keys are listed in order of creation with your primary key first and subkeys after.

In order to extract your SSH public key, run the following:

```shell
> user@workstation ~/ $ gpg -a --export-ssh-key 84FE2A5988AB6BA1 | xclip -selection clipboard
```

This will export your SSH public key to your clipboard. 

<div>
  <a href="configuring-the-ssh-agent-to-use-gpg.md">Previous</a>
  <a href="adding-a-new-ssh-key-to-your-github-account.md">Next</a>
</div>