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
  <a href="exporting-your-ssh-public-key.md" class="nav-link">Previous</a>
  <a href="testing-your-ssh-connection.md" class="nav-link">Next</a>
</div>