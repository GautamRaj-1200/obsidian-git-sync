## Q. How can you calculate upload progress of a file?
### A. Depends on the method used for the upload, the platform, and the tools involved
1. **Using JavaScript with XMLHttpRequest**
2. **Using JavaScript with Fetch API**
	- Fetch API does not natively support tracking progress, but you can use `ReadableStream` to achieve this.
3. **Using Axios for File Upload with Progress**
	- The `onUploadProgress` option tracks the progress of the uploaded file.