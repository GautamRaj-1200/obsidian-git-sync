## Apt Package Manager - Removing Programs Completely
-  **To uninstall a program while keeping its configuration files, use the following command:**`sudo apt remove <program_name>` 
	or
- **If you want to completely remove a program along with its configuration files, use the `purge` command**: `sudo apt purge <program_name>`
- **Clean Up Unused Packages**:`sudo apt autoremove`
- While `purge` removes most configuration files, some may remain in your home directory or elsewhere. You might need to manually delete these leftover files. Look for hidden files or directories (those starting with a dot) in your home directory related to the program you removed and delete them using: the command may vary depending on location and naming of directories `rm -rf ~/.config/<program_name>`
### Additional Cleanup Commands
- **Clear Package Cache**: If you're looking to free up space, you can clear out the local repository of retrieved package files with: `sudo apt clean`