# Configuring Git from the CLI

When setting up a new machine for development or personal use, one of the first things that you need to do is make sure that your git CLI is configured to comminicate with your remote, in this case, GitHub. 

In this guide, you will learn how to generate keys to authenticate your identity when connecting to GitHub from the git CLI, add those keys to your GitHub account, and set your machine up for contributing to repositories using your verified identity. 

In order to connect to GitHub from the git CLI you will be using GPG keys. GPG keys provide the option to generate SSH subkeys that can be used for authentication. This feature allows keys to be managed from a single tool, reducing the risk of mismanagement of keys while performing command line operations.

## Table of Contents

1. <a href="verifying-your-gpg-command-line-tools-installation.md">Verifying Your GPG Command Line Tools Installation</a>

2. <a href="generating-new-gpg-keys.md">Generating New GPG Keys</a>

3. <a href="generating-a-gpg-subkey-for-signing-commits-and-tags.md">Generating a GPG Subkey for Signing Commits and Tags</a>

4. <a href="configuring-the-git-cli-to-sign-commits-and-tags.md">Configuring the Git CLI to Sign Commits and Tags</a>

5. <a href="adding-your-gpg-signing-key-to-github.md">Adding your GPG Signing Key to GitHub</a>

6. <a href="generating-a-gpg-subkey-for-ssh.md">Generating a GPG Subkey for SSH</a>

7. <a href="configuring-the-ssh-agent-to-use-gpg.md">Configuring the SSH Agent to Use GPG</a>

8. <a href="exporting-your-ssh-public-key.md">Exporting Your SSH Public Key</a>

9. <a href="adding-a-new-ssh-key-to-your-github-account.md">Adding a New SSH Key to Your GitHub Account</a>

10. <a href="testing-your-ssh-connection.md">Testing Your SSH Connection</a>

<style>
    .bottom-nav {
        display: flex; 
        justify-content: flex-end; 
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
  <a href="verifying-your-gpg-command-line-tools-installation.md" class="nav-link">Next</a>
</div>