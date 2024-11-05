## /usr/bin/gh auth git-credential get: 1: /usr/bin/gh: not found
- The error message `/usr/bin/gh auth git-credential get: 1: /usr/bin/gh: not found` indicates that the system cannot find the GitHub CLI (`gh`) executable at the specified path. This typically happens for a few reasons:
	1. **GitHub CLI Not Installed**: The `gh` command may not be installed on your system. You can verify this by running `which gh` or `gh --version`. If it's not installed, you'll need to install it using your package manager (e.g., `apt`, `brew`, etc.) or download it from the GitHub releases page.
	2. **Incorrect Path**:If `gh` is installed but located in a different directory, the system won't be able to find it at `/usr/bin/gh`. You can check where it is installed and update your `$PATH` variable accordingly.
	3. **Installation Issues**: Sometimes, the installation might have been corrupted or incomplete. Reinstalling the GitHub CLI can resolve this issue. If you used a package manager like `snap`, consider uninstalling it and reinstalling using the official instructions from GitHub
	4. **Configuration Errors**: If you have recently made changes to your Git configuration or authentication settings, ensure that they are correct. You might need to run `gh auth login` again to set up your authentication properly

> In My case it was appearing whenever i tried to push, but I didn't have `gh cli` installed, but I had installed it earlier, so i think there was some misconfiguration. So what I did
	
- **Remove GitHub CLI References from Git Configuration**: `git config --global --unset credential.helper`
- **After running this command, check if any credential helpers are still set:** `git config --list --show-origin | grep credential`
- **After this: I had to remove the `.gitconfig`** file too
- **Set Up a Different Credential Helper (Optional)**: **cache** or **store**
	- `git config --global credential.helper cache # Temporarily caches credentials in memory.`
	- ``