# Simple server deployed localy

This is going to be as simple as running a simple app locally. For this we're going to use [`Node.js`](https://nodejs.org/en/).


The server is as simple as this:
```javascript
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```
Running the server:
```bash
$ node app.js
Server running at http://127.0.0.1:3000/
```
