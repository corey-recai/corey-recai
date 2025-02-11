#### Generating a GPG Subkey for SSH

Now that you have your GPG keyring, you are going to generate a GPG subkey for SSH that will be used for authentication when connecting to GitHub.

You will need the ID of your primary GPG key in order to begin this process.

To find your primary key pair, run the following:

```shell
> user@workstation ~/ $ gpg -K --keyid-format=long
...
------------------------------------
sec   ed25519/3AA5C34371567BD2 2025-02-06 [SC]
uid                          username (authentication and signing keyring for GitHub) <verified-github-email@example.com>
ssb   cv25519/4BB6D45482678BE3 2025-02-06 [E]
ssb   cv25519/5269150E95DAC3EB 2025-02-06 [S]
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

1. The type of key you want. You are generating an ed25519 key for authentication, select `ECC (set your own capabilities)`, and press <kbd>Enter</kbd>.

2. You will now be asked to edit the possible actions for the subkey. You should be presented with the following prompt:
    ```
    Possible actions for this ECC key: Sign Authenticate
    Current allowed actions: Sign

   (S) Toggle the sign capability
   (A) Toggle the authenticate capability
   (Q) Finished
    ```
    type S to turn the signing capability off, and press <kbd>Enter</kbd> to continue.

    You will now be present with the same prompt, howeverm the `Current allowed actions:` should be empty:
    ```
    Possible actions for this ECC key: Sign Authenticate
    Current allowed actions:

   (S) Toggle the sign capability
   (A) Toggle the authenticate capability
   (Q) Finished
    ```
    type <kbd>A</kbd> to turn the authentication capability on, and press <kbd>Enter</kbd> to continue.

    You will be presented with the same prompt again, however, the `Current allowed actions:` should now reflect `Authenticate`.
    ```
    Possible actions for this ECC key: Sign Authenticate
    Current allowed actions: Authenticate

   (S) Toggle the sign capability
   (A) Toggle the authenticate capability
   (Q) Finished
    ``` 
    Once you have confirmed that the authentication capability has been turned on, type <kbd>Q</kbd> and press <kbd>Enter</kbd> to continue.

3. The elliptic curve you want. Select `Curve 25519`, if it is not the default. Otherwise, press <kbd>Enter</kbd> to accept the default.

4. How long you want the key to be valid for. For the purpose of this guide, you are going to select `0 = key does not expire`, if it is not the default. Otherwise, press <kbd>Enter</kbd> to accept the default. You will then be asked to confirm the expiry, type <kbd>y</kbd> and then press <kbd>Enter</kbd> to confirm your choice.

5. You will then be asked to confirm the creation of the subkey, type <kbd>y</kbd> and then press <kbd>Enter</kbd> to confirm your choice.

6. You will be presented with an on-screen prompt asking you to enter the passphrase that you created for your primary key when generating your GPG keys. Enter the passphrase and confirm to somplete the subkey creation process.

Once the subkey has been created, you will be returned to the GPG CLI.

To save your changes and your subkey, run:

```
gpg> save
```

The GPG CLI will now exit and you will be returned to your user shell.

<div>
  <a href="adding-your-gpg-signing-key-to-github.md">Previous</a>
  <a href="configuring-the-ssh-agent-to-use-gpg.md">Next</a>
</div>