1. **How would you manage credentials in git?**
	1. **Check Current Configuration**:Run the following command to see if your `username`, `email`, or `credential.helper` is set: `git config --list`
	2. **Set Username and Email**:If they are not set, you can configure them globally with: 
	```bash
	git config --global user.name "your username" 
	git config --global user.email "your email"
	```
		This ensures that your commits are associated with the correct identity across all repositories on your machine
	1. 