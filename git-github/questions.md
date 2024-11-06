1. **How would you manage credentials in git?**
	1. **Check Current Configuration**:Run the following command to see if your `username`, `email`, or `credential.helper` is set: `git config --list`
	2. **Set Username and Email**:If they are not set, you can configure them globally with: This ensures that your commits are associated with the correct identity across all repositories on your machine
	```bash
	git config --global user.name "your username" 
	git config --global user.email "your email"
	```
	3. **Configure Credential Helper**:  To manage credentials, you can use either `cache` or `store`. Here, we will use `store`, which saves credentials to a file: This command specifies that Git should save your credentials in a file located at `~/.git-credentials`
	```bash
	git config --global credential.helper store --file ~/.git-credentials
	```
	4. **Authenticate When Pushing**:  The next time you push to a repository, Git will prompt you for your username and Personal Access Token (PAT). Enter these to authenticate
	5. 