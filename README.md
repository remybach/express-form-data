# express-form-data
Module to parse multipart/form data. Based on [connect-multiparty](https://github.com/expressjs/connect-multiparty)

# Install 
`npm install express-form-data`

# Example
```js
const formData = require("express-form-data");
const express = require("express");
const os = require("os");
const app = express();

/**
 * Options are the same as multiparty takes.
 * But there is a new option "autoClean" to clean all files in "uploadDir" folder after the response.
 * By default, it is "false".
 */
const options = {
  uploadDir: os.tmpdir(),
  autoClean: true
};

// parse data with connect-multiparty. 
app.use(formData.parse(options));
// clear from the request and delete all empty files (size == 0)
app.use(formData.format());
// change file objects to stream.Readable 
app.use(formData.stream());
// union body and files
app.use(formData.union());
```

After this we can see in req:  
* req.files = {...} all files  
* req.body = {...} all data including files (or streams if you use .stream())
