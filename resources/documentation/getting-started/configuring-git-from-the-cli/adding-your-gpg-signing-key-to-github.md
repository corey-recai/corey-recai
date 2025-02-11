#### Adding your GPG Signing Key to GitHub

You now need to add your GPG public key to GitHub in order to verify your commits and tags once they are pushed to the remote to do this you need to export your GPG public key.

You will first need the ID of the subkey that you created for signing commits and tags, retrieve it by running:

```shell
> user@workstation ~/ $ gpg -K --keyid-format=long
...
------------------------------------
sec   ed25519/3AA5C34371567BD2 2025-02-06 [SC]
uid                          username (authentication and signing keyring for GitHub) <verified-github-email@example.com>
ssb   cv25519/4BB6D45482678BE3 2025-02-06 [E]
ssb   cv25519/5269150E95DAC3EB 2025-02-06 [S]
```

Then export your GPG public key by running: 
```
> user@workstation ~/ $ gpg -a --export 3AA5C34371567BD2 | xclip -selection clipboard
```

Add your GPG public key to GitHub by performing the following steps:

1. In the upper-right corner of any page on GitHub, click your profile photo, then click Settings.

2. In the "Access" section of the sidebar, click SSH and GPG keys.

3. Next to the "GPG keys" header, click New GPG key.

4. In the "Title" field, add a descriptive label for your GPG key, that identifies the machine or service it is being used for. For example, if you're using a personal laptop, you might call this key "personal-laptop".

5. In the "Key" field, paste the GPG key you copied when you generated your GPG key.

6. Click Add GPG key.

7. If prompted, comfirm access to your GitHub Account.

<div>
  <a href="configuring-the-git-cli-to-sign-commits-and-tags.md">Previous</a>
  <a href="generating-a-gpg-subkey-for-ssh.md">Next</a>
</div>