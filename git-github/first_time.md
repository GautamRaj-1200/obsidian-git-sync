## Steps to Commit and Push to GitHub for the First Time
1. **Initialize a New Git Repository**:
```bash
git init
```
2. **Create and Switch to the Main Branch**:
```bash
git branch -M main
```
3. **Stage Your Changes**:  Add all files in the current directory to the staging area:
```bash
git add .
```
4. **Commit Your Changes**: Make your initial commit with a message:
```bash
git commit -m "initial commit"
```
5. **Configure Your User Information** (if prompted):  If you haven't set your username and email globally, you may be asked to do so. Run the following commands:
```bash
git config --global user.name "your username" 
git config --global user.email "your email"
```
6. **Set Up Credential Helper** (Optional):  To avoid entering your credentials every time, you can store them securely:
```bash
git config --global credential.helper store --file ~/.my-credentials
```
7. **Add Remote Repository**:  Replace `USERNAME` and `REPOSITORY` with your GitHub username and the name of your repository:
```bash
git remote add origin https://github.com/USERNAME/REPOSITORY.git
```
8. **Push Your Changes**:  When you push for the first time, use the following command:
```bash
git push -u origin main
```
9. **Authenticate Using Personal Access Token**:
	- When prompted for your username, enter your GitHub username.
	- For the password, enter your Personal Access Token (PAT) instead of your GitHub password.

### Creating PAT
1. **Log in to GitHub**.
2. Click on your profile picture in the top right corner and select **Settings**.
3. In the left sidebar, click on **Developer settings**, then select **Personal access tokens**.
4. Click on **Generate new token**.
5. Provide a descriptive name in the "Note" field.
6. Select the scopes you need (for general Git operations, select `repo`).
7. Click on **Generate token**.
8. Copy the generated token immediately; it will not be displayed again.