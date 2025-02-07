# Configuring Git from the CLI

When setting up a new machine for development or personal use, one of the first things that you need to do is make sure that your git CLI is configured to comminicate with your remote, in this case, GitHub. 

In this guide, you will learn how to generate keys to authenticate your identity when connecting to GitHub from the git CLI, add those keys to your GitHub account, and set your machine up for contributing to repositories using your verified identity. 

In order to connect to GitHub from the git CLI you will be using GPG keys. GPG keys provide the option to generate SSH subkeys that can be used for authentication. This feature allows keys to be managed from a single tool, reducing the risk of mismanagement of keys while performing command line operations.

#### Verifying Your GPG Command Line Tools Installation

Before you are able to generate your GPG keys, you will need to confirm that you have the [GPG command line tools](https://www.gnupg.org/download/) installed.

Check that you have the GPG command line tools installed by running:

```shell
> user@workstation ~/ $ which gpg
/usr/bin/gpg
```

If this command returns:

```
which: no gpg in ($PATH)
```

Then you either do not have the GPG command line tools installed, or your `PATH` does not point to the location where the GPG command line tools are installed.

Once you have confirmed that you have the GPG command line tools installed, you need to check the version. This will inform you of which command you need to run in the following steps.

Check the version of the GPG command line tools that you have installed by running:

```shell
> user@workstation ~/ $ gpg --version
gpg (GnuPG) 2.4.7
libgcrypt 1.11.0
Copyright (C) 2024 g10 Code GmbH
...
```

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

#### Configuring the SSH Agent to Use GPG

Now that you have generated a new SSH key, when you connect to GitHub from the git CLI your machine will need to use your private key, stored in the GPG keyring to authenticate your connection. 

By default the ssh-agent looks for private keys in a certain location, so you will need to tell the ssh-agent where your GPG keyring is located. 

There are several ways to configure the ssh-agent to use GPG, however, we will be using an method that tells the ssh-agent to authenticate using the authentication socket provided by the gpg-agent.

To get started we will need to enable SSH support in the gpg-agent by editing the GPG configuration file, you can do this by running:

```shell
user@workstation ~/ $ echo enable-ssh-support >> $HOME/.gnupg/gpg-agent.conf
```

Next, you will need to update your shell profile or rc file with the following:

```shell
if [ "${gnupg_SSH_AUTH_SOCK_by:-0}" -ne $$ ]; then
  export SSH_AUTH_SOCK="$(gpgconf --list-dirs agent-ssh-socket)"
fi
export GPG_TTY=$(tty)
gpg-connect-agent updatestartuptty /bye >/dev/null
```

Which will, on startup, set the gpg-agent SSH authentication socket, and update the terminal device that the gpg-connect-agent uses for input/output.

After editing your shells startup instructions, you need to add your GPG subkey to the `sshcontrol` list to let the gpg-agent know that it is an SSH key being used for authentication.

You will need the keygrip of your authentication subkey in order to do this, retrieve it by running:

```shell
user@workstation ~/ $ gpg -k --with-keygrip --keyid-format=long
...
------------------------------------
sec   ed25519/3AA5C34371567BD2 2025-02-06 [SC]
      Keygrip = 22DBE374608C6220B321D3A2543F3806FF63A49D
uid                          username (authentication and signing keyring for GitHub) <verified-github-email@example.com>
ssb   cv25519/4BB6D45482678BE3 2025-02-06 [E]
      Keygrip = A55719832AF939C531BACFFABB2A47B52FFBBF43
ssb   cv25519/5269150E95DAC3EB 2025-02-06 [S]
      Keygrip = 986DD7B2CC3129E9E8ADAC54988A535BE615F67E
ssb   cv25519/84FE2A5988AB6BA1 2025-02-06 [A]
      Keygrip = 1C7128A0EDFB0A7BAE1FB3C44E8CC7FC570F6586
```

Add your authentication subkey keygrip to the `sshcontrol` list by running the following:

```shell
user@workstation ~/ $ echo 1C7128A0EDFB0A7BAE1FB3C44E8CC7FC570F6586 >> ~/.gnupg/sshcontrol
```

Confirm that your subkey is present in the SSH identities list by running:

```shell
user@workstation ~/ $ ssh-add -l
256 SHA256:bCVzkgaoGSqJC89hZ/8gclTn7ENN/dJ+mZBBw2zJFuI (none) (ED25519)
```

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

#### Adding a New SSH Key to Your GitHub Account

Now, navigate to your GitHub account in your web browser and perform the following:

1. In the upper-right corner of any page on GitHub, click your profile photo, then click Settings.

2. In the "Access" section of the sidebar, click SSH and GPG keys.

3. Click New SSH key or Add SSH key.

4. In the "Title" field, add a descriptive label for the new key, that identifies the machine or service it is being used for. For example, if you're using a personal laptop, you might call this key "personal-laptop".

5. The type of key is authentication.

6. In the "Key" field, paste your public key.

7. Click Add SSH Key.

8. If prompted, comfirm access to your GitHub Account.

#### Testing Your SSH Connection

With your SSH key added to GitHub, and the ssh-agent configured to use GPG for SSH connections, you are now ready to test your SSH connection to github.com and authenticate your identity.

Run the following, to test your connection to github.com via SSH.

```shell
user@workstation ~/ $ ssh -T git@github.com
```

If you configured everything properly you will recieve a prompt to enter your passphrase, once you have entered your passphrase correctly, you should recieve the following output.

```
Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```