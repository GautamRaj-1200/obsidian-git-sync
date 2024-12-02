## Q. How can you input a file or files in html
### A. Using `<input type="file">`
- It lets user choose one or more files.

## Q. What are the things we can do once file(s) is chosen?
### A. Two things:
- Upload to a server using **Form Submission**
- Manipulate using JS Code and the **FILE API**

## Q. How to specify files type to accept?
### A. Using `accept` attribute
- Using a comma separated string list of unique file type specifiers
- Ex: `accept=".doc,.docx,.xml,application/msword"`
- Ex: `accept=".pdf"`
- Ex: `accept=".doc"`
- Ex: `accept="image/* , .pdf"` - _image/ *: means any image file_
## Q. How to allow users to select more than 1 file?
### A. Using `multiple` attribute
- When the [`multiple`](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/multiple) Boolean attribute is specified, the file input allows the user to select more than one file.
## Q. What does the value attribute of a file input type contain?
### A. A string that represents the path of the selected file(s)
- Empty "" if no file is selected.
- When multiple files is selected the ***value represents the first file*** in the list.
- To identify and access other files: **FILE API needs to be used**: Use `HTMLInputElement.files` property
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

