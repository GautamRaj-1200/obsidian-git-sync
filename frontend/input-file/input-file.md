## Q. How can you input a file or files in html
### A. Using `<input type="file">`
- It lets user choose one or more files.
___
## Q. What are the things we can do once file(s) is chosen?
### A. Two things:
- Upload to a server using **Form Submission**
- Manipulate using JS Code and the **FILE API**
___
## Q. How to specify files type to accept?
### A. Using `accept` attribute
- Using a comma separated string list of unique file type specifiers
- Ex: `accept=".doc,.docx,.xml,application/msword"`
- Ex: `accept=".pdf"`
- Ex: `accept=".doc"`
- Ex: `accept="image/png"` or `accept=".png"` (Both are same) 
- Ex: `accept="image/* , .pdf"` - _image/ *: means any image file_
- **NOTE**: Make sure that the `accept` attribute is backed up by appropriate server-side validation as the `accept` attribute doesn't validate the types of the selected files
___
## Q. How to allow users to select more than 1 file?
### A. Using `multiple` attribute
- When the [`multiple`](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/multiple) Boolean attribute is specified, the file input allows the user to select more than one file.
___
## Q. What does the value attribute of a file input type contain?
### A. A string that represents the path of the selected file(s)
- Empty "" if no file is selected.
- When multiple files is selected the ***value represents the first file*** in the list.
- To identify and access other files: **FILE API needs to be used**: Use `HTMLInputElement.files` property
___
## Q. How to access different information of a file, such as it's name, size etc?
### A. File object contains these information
- The following information is contained in each File object
	- `name`: the file's name
	- `size`: the size of file in **bytes**
	- `type`: the file's MIME type
	- `lastModified`: A number specifying the date and time at which the file was last modified, in milliseconds since the UNIX epoch (January 1, 1970, at midnight).
___
## Q. When we select a file, it's path is contained in the value attribute? Isn't it a security concern? How is it handled?
### A. Yes, when a user selects a file through an HTML `<input type="file">` form, the file path (or file name) is initially included in the `value` attribute of the input field. However, this **file path** behavior has been a source of concern, and modern browsers have implemented measures to mitigate the associated security risks.

To mitigate these risks, modern browsers **sanitize** the file path and only expose the **file name**, effectively blocking the ability to see the actual path.
1. **Fake Path (`C:\fakepath\` or similar):**
    - Instead of returning the actual file path, browsers return a fake path, such as `C:\fakepath\fileName.ext`, where `fileName.ext` is the actual name of the file the user selected. This prevents websites from seeing where the file is stored on the user's system.
    - **For example:**
        - **Before sanitization:** `C:\Users\John\Documents\Files\myphoto.png`
        - **After sanitization:** `C:\fakepath\myphoto.png`
    - This ensures that only the file name is visible, and not its directory structure.
2. **No Access to File Path:**
    - Browsers have deliberately disabled the ability for websites to access the real file path to enhance privacy and security. The `value` attribute of the `<input type="file">` element only contains the file name (or a sanitized fake path), not the entire file system path.
3. **File Name Exposure:**
    - While the actual path is hidden, the **file name** is still exposed. This is important because the server needs to know what file the user has selected to properly process the upload. However, the file name alone does not provide any information about where the file resides on the user's computer.
___
## Styling file input
- By default, it does not look great.
- So, we do the following:
-  **Custom Layer:** We create a custom button or layer above the file input using absolute positioning, effectively hiding the default input.
- **Pointer Events:** We set `pointer-events: none` on the custom layer so that interactions with the file input are passed through to the actual file input, allowing the file selection to function as normal.
___
