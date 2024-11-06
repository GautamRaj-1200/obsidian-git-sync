###  1. **How would you manage credentials in git?**
	- First run the following command to see if the *username*, *email* or *helper* is set or not.
	- If not, then set them using
	```bash
	git config --global user.name "your username" 
	git config --global user.email "your email"
	git config --global credential.helper store --file ~/.my-credentials
	```
	- For credentials we can use `cache` or `store`
	- Then try to push, it will ask for authentication, authenticate using username and Personal Access Token.
- 
