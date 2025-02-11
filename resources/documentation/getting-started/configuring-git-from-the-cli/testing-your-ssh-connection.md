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

<style>
    .bottom-nav {
        display: flex; 
        justify-content: flex-start; 
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
  <a href="adding-a-new-ssh-key-to-your-github-account.md" class="nav-link">Previous</a>
</div>