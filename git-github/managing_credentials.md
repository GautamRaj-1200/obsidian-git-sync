-  **How would you manage credentials in git?**
	1. **Check Current Configuration**:Run the following command to see if your `username`, `email`, or `credential.helper` is set: 
	```bash
	git config --list
	```
	1. **Set Username and Email**:If they are not set, you can configure them globally with: This ensures that your commits are associated with the correct identity across all repositories on your machine
	```bash
	git config --global user.name "your username" 
	git config --global user.email "your email"
	```
	3. **Configure Credential Helper**:  To manage credentials, you can use either `cache` or `store`. Here, we will use `store`, which saves credentials to a file: This command specifies that Git should save your credentials in a file located at `~/.git-credentials`
	```bash
	git config --global credential.helper store --file ~/.git-credentials
	```
	4. **Authenticate When Pushing**:  The next time you push to a repository, Git will prompt you for your username and Personal Access Token (PAT). Enter these to authenticate
	5. **Removing Existing Credentials**:  If you need to remove existing credentials and start fresh, execute the following commands:This will clear any previously set username, email, and credential helper settings, as well as delete the stored credentials file
	```bash
	git config --global --unset-all user.name 
	git config --global --unset-all user.email 
	git config --global --unset credential.helper 
	rm ~/.git-credentials
	```
	6. **Reconfigure After Removal**:  
    After clearing the old configurations, you can set them again using the commands from steps 2 and 3.
    7. **Additional Notes**
	- **Credential Helpers**: The `cache` helper temporarily stores credentials in memory for a specified duration (default is 15 minutes), while `store` saves them permanently until manually removed.
	- **Local vs Global Configuration**: You can also set username and email for specific repositories by omitting the `--global` flag and running the commands inside the repository directory