-  Create an **Applications** folder in the home directory.
- Let's take example of Obsidian
	- File name : `Obsidian.AppImage`
- Create a folder inside `Applications` folder
	-  `obsidian`
		- Move `Obsidian.AppImage` here
		- Also add a logo image if you like
- Give executable permission to AppImage
	- `sudo chmod 755 Obsidian.AppImage`
- Go to `nano ~/.local/share/applications/obsidian.desktop`
- Write this 
```text
[Desktop Entry]
Name=Obsidian
Exec=/home/coding-stage/Applications/obsidian/Obsidian.AppImage
Icon=/home/coding-stage/Applications/obsidian/Obsidian-logo.jpeg
Type=Application
```
- Save and Exit
- Then run the following in terminal
`sudo update-desktop-database ~/.local/share/applications`