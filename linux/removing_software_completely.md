## Apt Package Manager - Removing Programs Completely
-  **To uninstall a program while keeping its configuration files, use the following command:**`sudo apt remove <program_name>` 
	or
- **If you want to completely remove a program along with its configuration files, use the `purge` command**: `sudo apt purge <program_name>`
- **Clean Up Unused Packages**:`sudo apt autoremove`
- Any configuration files in home directory has to be manually deleted thereafter.