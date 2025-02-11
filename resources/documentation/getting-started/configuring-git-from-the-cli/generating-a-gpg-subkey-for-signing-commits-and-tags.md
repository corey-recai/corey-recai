#### Generating a GPG Subkey for Signing Commits and Tags

Now that you have your GPG keyring, you are going to generate a GPG subkey that will be used for signing commits and tags.

You will need the ID of your primary GPG key in order to begin this process.

To find your primary key pair, run the following:

```shell
> user@workstation ~/ $ gpg -K --keyid-format=long
...
------------------------------------
sec   ed25519/3AA5C34371567BD2 2025-02-06 [SC]
uid                          username (authentication and signing keyring for GitHub) <verified-github-email@example.com>
ssb   cv25519/4BB6D45482678BE3 2025-02-06 [E]
```

Next, edit your GPG key by running the following:

```shell
> user@workstation ~/ $ gpg --expert --edit-key 3AA5C34371567BD2
...
gpg>
```

This will bring you into the GPG CLI.

Add a new subkey by running:

```shell
gpg> addkey
```

After you run the command to add a new subkey, you will be presented with the following prompts:

1. The type of key you want. You are generating an ed25519 key for authentication, select `ECC (sign only)`, and press <kbd>Enter</kbd>.

2. The elliptic curve you want. Select `Curve 25519`, if it is not the default. Otherwise, press <kbd>Enter</kbd> to accept the default.

3. How long you want the key to be valid for. For the purpose of this guide, you are going to select `0 = key does not expire`, if it is not the default. Otherwise, press <kbd>Enter</kbd> to accept the default. You will be asked to confirm the expiry, type <kbd>y</kbd> and then press <kbd>Enter</kbd> to confirm your choice.

4. You will be asked to confirm the creation of the subkey, type <kbd>y</kbd> and then press <kbd>Enter</kbd> to confirm your choice.

5. You will be presented with an on-screen prompt asking you to enter the passphrase that you created for your primary key when generating your GPG keys. Enter the passphrase and confirm to somplete the subkey creation process.

Once the subkey has been created, you will be returned to the GPG CLI.

To save your changes and your subkey, run:

```
gpg> save
```

The GPG CLI will now exit and you will be returned to your user shell.

<style>
    .bottom-nav {
        display: flex; 
        justify-content: space-between; 
        border: 1px solid #373b42; 
        border-radius: 1em; 
        padding: 0.5em;
    }
    .nav-link{
        border: 1px solid #373b42; 
        border-radius: 1em; 
        padding: 0.5em; 
        width: 8em; 
        height: 2.5em; 
        background-color: #21262d;
        cursor: pointer;
        color: #fff;
        align-content: center;
        text-align: center; 
    }

    .nav-link:hover {
        text-decoration: none;
        color: #aeb4b9;
    }
</style>
<div class="bottom-nav">
  <a href="generating-new-gpg-keys.md" class="nav-link">Previous</a>
  <a href="configuring-the-git-cli-to-sign-commits-and-tags.md" class="nav-link">Next</a>
</div>