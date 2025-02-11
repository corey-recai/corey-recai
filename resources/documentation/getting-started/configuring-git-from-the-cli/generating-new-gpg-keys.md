#### Generating New GPG Keys

Once you have confirmed the version of the GPG command line tools that you have installed, you can proceed with generating a new set of GPG keys.

You are going to generate your GPG keys using the ed25519 algorithm.

To generate a new set of GPG keys, run the following command:

```shell
> user@workstation ~/ $ gpg --full-generate-key
```

If you are using a version of the GPG command line tools prior to version 2.1.17, run the following command, and skip to step 4:

```shell
> user@workstation ~/ $ gpg --default-new-key-algo ed25519 --gen-key
```
After you run the command to begin the GPG key generation process, you will be presented with the following prompts:

1. The type of key you want. You are generating an ed25519 key for both authentication and signing, select `ECC (sign and encrypt)`, if it is not the default. Otherwise, press <kbd>Enter</kbd> to accept the default.

2. The elliptic curve you want. Select `Curve 25519`, if it is not the default. Otherwise, press <kbd>Enter</kbd> to accept the default.

3. How long you want the key to be valid for. For the purpose of this guide, you are going to select `0 = key does not expire`, if it is not the default. Otherwise, press <kbd>Enter</kbd> to accept the default. You will then be asked to confirm the expiry, type <kbd>y</kbd> and then press <kbd>Enter</kbd> to confirm your choice.

4. You will now be asked to create a userID to identify your key. The userID will start with the `Real name:` field, you are going to use your GitHub username for this field. Type your GitHub username, and press <kbd>Enter</kbd> to confirm.

5. The next field in the userID is your `Email address:`, you are going to use the email address that you have verified with GitHub. Type your verified GitHub email address, and press <kbd>Enter</kbd> to confirm.

6. The final field in the userID is a `Comment:`, this will specify the purpose of the key, enter the following:
    ```
    authentication and signing keyring for GitHub
    ```
    then press <kbd>Enter</kbd> to confirm.

7. You will now be given the option to change the information in the userID, confirm the information in the userID, or quit the key creation process; type <kbd>O</kbd> and press <kbd>Enter</kbd> to confirm, once you have ensured that the information is correct.

8. Your keys will now be generated and you will recieve and on-screen prompt to enter a passphrase to secure your keys. Enter the same secure passphrase in both fields and press confirm to complete the creation process.

<div>
  <a href="verifying-your-gpg-command-line-tools-installation.md">Previous</a>
  <a href="generating-a-gpg-subkey-for-signing-commits-and-tags.md">Next</a>
</div>