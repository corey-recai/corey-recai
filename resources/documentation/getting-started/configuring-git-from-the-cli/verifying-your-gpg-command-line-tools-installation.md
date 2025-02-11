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
  <a href="README.md" class="nav-link">Previous</a>
  <a href="generating-new-gpg-keys.md" class="nav-link">Next</a>
</div>