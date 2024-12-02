## Q. How can you input a file or files in html
### A. Using `<input type="file">`
- It lets user choose one or more files.

## Q. What are the things we can do once file(s) is chosen?
### A. Two things:
- Upload to a server using **Form Submission**
- Manipulate using JS Code and the **FILE API**

## Q. How to specify files type to accept?
### A. Using `accept` attribute

## Q. What does the value attribute of a file input type contain?
### A. A string that represents the path of the selected file(s)
- Empty "" if no file is selected.
- When multiple files is selected the ***value represents the first file*** in the list.
- To identify and access other files: **FILE API needs to be used**: Use `HTMLInputElement.files` property

## Q. When we select a file, it's path is contained in the value attribute? Isn't it a security concern? How is it handled?
- To mitigate these risks, modern browsers **sanitize** the file path and only expose the **file name**, effectively blocking the ability to see the actual path.
1. **Fake Path (`C:\fakepath\` or similar):**    
    - Instead of returning the actual file path, browsers return a fake path, such as `C:\fakepath\fileName.ext`, where `fileName.ext` is the actual name of the file the user selected. This prevents websites from seeing where the file is stored on the user's system.
    - **For example:**
        
        - **Before sanitization:** `C:\Users\John\Documents\Files\myphoto.png`
        - **After sanitization:** `C:\fakepath\myphoto.png`
    - This ensures that only the file name is visible, and not its directory structure.