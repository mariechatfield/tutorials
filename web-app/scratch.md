Express.js: http://expressjs.com/

`npm install --save express`
`mkdir -p backend/app`
`touch backend/app/server.js`

```js
const express = require('express');
const app = express();

const DEFAULT_PORT = 3000;

app.get('/', function (req, res) {
  res.send('Hello World!');
});

const server = app.listen(process.env.port || DEFAULT_PORT, function () {
  const port = server.address().port;
  console.log(`Server listening on port ${port}!`);
});
```

nodemon: https://nodemon.io/

`npm install --save nodemon`

```json
   "backend": "PORT=3000 nodemon backend/app/server.js --ignore ./app/ --ignore tmp/ --ignore test/",
    "frontend": "ember server --proxy http://127.0.0.1:3000"
```

`npm run backend`

`http://localhost:3000/`: `Hello World!`

`Hello World!` --> `Hello marie!` and reload browser page

```js
const greeting = req.query.name !== undefined ? 
    `Hello ${req.query.name}!` : 
    `Hello stranger!`;

res.send(greeting);
```

`http://localhost:3000/?name=marie`

`npm run frontend`
