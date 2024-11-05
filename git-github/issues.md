## /usr/bin/gh auth git-credential get: 1: /usr/bin/gh: not found
- The error message `/usr/bin/gh auth git-credential get: 1: /usr/bin/gh: not found` indicates that the system cannot find the GitHub CLI (`gh`) executable at the specified path. This typically happens for a few reasons:
	1. **GitHub CLI Not Installed**: The `gh` command may not be installed on your system. You can verify this by running `which gh` or `gh --version`. If it's not installed, you'll need to install it using your package manager (e.g., `apt`, `brew`, etc.) or download it from the GitHub releases page.
	2. **Incorrect Path**:If `gh` is installed but located in a different directory, the system won't be able to find it at `/usr/bin/gh`. You can check where it is installed and update your `$PATH` variable accordingly.
	3. **Installation Issues**: Sometimes, the installation might have been corrupted or incomplete. Reinstalling the GitHub CLI can resolve this issue. If you used a package manager like `snap`, consider uninstalling it and reinstalling using the official instructions from GitHub
	4. **Configuration Errors**: If you have recently made changes to your Git configuration or authentication settings, ensure that they are correct. You might need to run `gh auth login` again to set up your authentication properly

> In My case it was appearing whenever i tried to push, but I didn't have `gh cli` installed, but I had installed it earlier, so i think there was some misconfiguration. So what I did
	
- **Remove GitHub CLI References from Git Configuration**: `git config --global --unset credential.helper`
- **After running this command, check if any credential helpers are still set:** `git config --list --show-origin | grep credential`
- **Clean Up Configuration Files**:  
	Additionally, you should remove any leftover configuration files related to `gh`. Delete the following directories if they exist:
	```
	rm -rf ~/.config/gh rm -rf ~/.local/state/gh rm -rf ~/.local/share/gh
	```
- Now try to push, You should now be prompted for your username and password (or personal access token) without any reference to `gh`.
- Even after this, i was getting the same error
- **After this: I had to remove the `.gitconfig`** file too or you can try doing the following

**Steps to Fix the `.gitconfig`**
1. **Edit Your `.gitconfig` File**:  
    Open your `.gitconfig` file in a text editor. You can use any editor of your choice, such as `nano`, `vim`, or `gedit`. Here’s how to do it with `nano`:
```bash
nano ~/.gitconfig
```
    
2. **Remove or Comment Out the Credential Helpers**:  
    Locate the sections that reference `gh` for credential management. Your configuration currently might looks like this:
    
```bash
[credential "https://github.com"] 
helper =    
helper = !/usr/bin/gh auth git-credential 

[credential "https://gist.github.com"]     
helper =   
helper = !/usr/bin/gh auth git-credential
```

You can either delete these lines or comment them out by adding a `#` at the beginning of each line. The modified section should look like this:text
    
```bash
[credential "https://github.com"] 
# helper =    
# helper = !/usr/bin/gh auth git-credential 

[credential "https://gist.github.com"]     
# helper =   
# helper = !/usr/bin/gh auth git-credential
```
    
3. **Save and Exit**:  
    If you are using `nano`, save the changes by pressing `CTRL + O`, then exit with `CTRL + X`.
4. **Verify Changes**:  
    You can verify that the changes have been made by running:bash
    `git config --list --show-origin | grep credential`
    Ensure that there are no remaining references to `gh`.
5. **Push Your Code Again**:  
    Now try pushing your code again using Git:bash
    `git push origin main  # Replace 'main' with your branch name if different.`
    You should no longer see the error related to `/usr/bin/gh`.
- **Set Up a Different Credential Helper (Optional)**: **cache** or **store**
	- `git config --global credential.helper cache # Temporarily caches credentials in memory.`
	- `git config --global credential.helper store` - I use the store