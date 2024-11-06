1. **How would you manage credentials in git?**
	- First run the following command to see if the *username*, *email* or *helper* is set or not.
	```bash
	git config --list
	```
	- If not, then set them using
	```bash
	git config --global user.name "your username" 
	git config --global user.email "your email"
	git config --global credential.helper store --file ~/.git-credentials
	```
	- For credentials we can use `cache` or `store`. Here I am using store.
	- Then try to push, it will ask for authentication, authenticate using username and Personal Access Token.
	- If credentials are already there, then to remove credentials and start fresh
	```bash
	git config --global --unset-all user.name
	git config --global --unset-all user.email
	git config --global --unset credential.helper
	rm ~
	```
