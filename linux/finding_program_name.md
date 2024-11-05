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


### 3. Using the Application Menu
If the application is installed and visible in your desktop environment's application menu:
- **Right-click the application icon** and select **Properties**.
- Look for the **command** field, which will show you the executable name that can be used in the terminal.

### 4. Using System Monitoring Tools
You can use system monitoring tools like `top`, `htop`, or `Gnome System Monitor`:
- Start the application you want to identify.
- Open a system monitoring tool (e.g., `top`, `htop`, or `gnome-system-monitor`).
- Look for the application in the list of running processes. The command name should be displayed alongside other details.