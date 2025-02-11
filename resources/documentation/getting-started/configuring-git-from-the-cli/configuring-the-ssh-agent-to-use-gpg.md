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
  <a href="generating-a-gpg-subkey-for-ssh.md" class="nav-link">Previous</a>
  <a href="exporting-your-ssh-public-key.md" class="nav-link">Next</a>
</div>