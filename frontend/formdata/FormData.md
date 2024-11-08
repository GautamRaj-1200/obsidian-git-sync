## Introduction
- `FormData` in JavaScript is a useful interface for working with HTML forms, enabling us to easily construct and manipulate form data, especially when sending it via `fetch` or `XMLHttpRequest`.
- It simplifies handling form data by letting us **append** and **retrieve** *key-value* pairs, manage files, and handle encoded form data without needing to manually format it.
- `FormData` automatically sets the `Content-Type` to `multipart/form-data` when we send it with `fetch` or `XMLHttpRequest`.
- It’s particularly useful for sending binary data like images or files.