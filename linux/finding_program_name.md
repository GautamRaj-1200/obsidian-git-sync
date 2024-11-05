## Finding Program Name in Ubuntu

When managing software on Ubuntu or other Debian-based systems using the APT package manager, it is essential to know the exact name of the program you want to install, remove, or manage. Here are several methods to find the correct program name:

### 1. List all installed packages
- **dpkg**
	- `dpkg --list`
	- For a specific package: `dpkg --list | grep <partial_name>`
- **apt**
	- `apt list --installed`
	- For a specific package: `apt list --installed | grep <partial_name>`

### 2. Inspecting .desktop Files
- Applications in Linux often have corresponding `.desktop` files located in `/usr/share/applications` or `~/.local/share/applications`. These files define how applications are launched and include relevant information:
	- `grep Exec /usr/share/applications/*.desktop`
	- This command will display lines starting with `Exec=`, showing you the command used to launch each application.


##