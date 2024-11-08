## Introduction
- `FormData` in JavaScript is a useful interface for working with HTML forms, enabling us to easily construct and manipulate form data, especially when sending it via `fetch` or `XMLHttpRequest`.
- It simplifies handling form data by letting us **append** and **retrieve** *key-value* pairs, manage files, and handle encoded form data without needing to manually format it.
- `FormData` automatically sets the `Content-Type` to `multipart/form-data` when we send it with `fetch` or `XMLHttpRequest`.
- It’s particularly useful for sending binary data like images or files.

## Example
### html
```html
<form id="uploadForm">
  <input type="file" id="fileInput" />
  <button type="button" onclick="uploadFile()">Upload</button>
</form>
```

### js(frontend)
```js
function uploadFile() {
  // Get the file from the input field
  const fileInput = document.getElementById('fileInput');
  const file = fileInput.files[0]; // The selected file
  
  // Create a new FormData object
  const formData = new FormData();
  
  // Append the file to the FormData object
  formData.append('file', file); // 'file' is the key, file is the value

  // Send the FormData object to the server using fetch
  fetch('/upload', {
    method: 'POST',
    body: formData,  // Send the FormData as the body of the POST request
  })
  .then(response => response.json())
  .then(data => {
    console.log('File uploaded successfully', data);
  })
  .catch(error => {
    console.error('Error uploading file:', error);
  });
}
```
### js(backend)

```js
const express = require('express');
const multer = require('multer');
const path = require('path');

const app = express();
const port = 3000;

// Set up multer to save the uploaded file
const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, 'uploads/'); // Save files to 'uploads' directory
  },
  filename: function (req, file, cb) {
    cb(null, Date.now() + path.extname(file.originalname)); // Generate a unique filename
  },
});

const upload = multer({ storage: storage });

// Route to handle file upload
app.post('/upload', upload.single('file'), (req, res) => {
  // req.file contains the uploaded file
  console.log(req.file);
  res.json({ message: 'File uploaded successfully', file: req.file });
});

app.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});

```