---
layout: tutorial
title:  "JavaScript App | Step 4: Create a server with Express"
tutorial_overview: web-app
previous_step: step3.html
next_step: step5.html
---

---

## Pre-requisities

| You should... | What to Review |
|------------ |-------- |
| ... have created a new Ember app using Ember CLI | [Step 2](step2.html) |
| ... be running your Ember app locally | [Step 2](step2.html) |
| ... have added routes and templates to your Ember app | [Step 3](step3.html) |

---

### Install Express

[Express](http://expressjs.com/) is a simple, powerful framework for creating web servers on top of Node. We can install it with npm:

`npm install express --save`

That command should be run inside `hello-world`. Using the `--save` option will add `express` to the list of dependencies of our application. Whenever we attempt to use our app or run it on another machine, we'll need to install all its dependencies before we can run anything.

The `express` package doesn't ship with a CLI app, so we can't check a version on the command line like we've done with other installations. But we can verify that express was added as a dependency to our `package.json` file:

```bash
~/projects/hello-world $ git diff
diff --git a/package.json b/package.json
index e462835..dc84780 100644
--- a/package.json
+++ b/package.json
@@ -39,5 +39,8 @@
     "ember-load-initializers": "^0.5.1",
     "ember-resolver": "^2.0.3",
     "loader.js": "^4.0.10"
+  },
+  "dependencies": {
+    "express": "^4.14.0"
   }
 }
```

### Create a simple server using Express

Now that we've built out our client side app just a bit, let's work on the server. We'll add our back end server in the same directory as our client side application.

Ember has stricter file structure expectations than Node/Express does, so we'll just nest all our backend code under a `backend` directory. We'll probably want to differentiate between app and test code for the server at some point, so our file structure will look like this:

```
_ hello_world
 |_ app        (Ember)
 |_ backend
   |_ app      (server)
   |_ test     (server)
 |_ test       (Ember)
```

To get started, let's create a `backend/app` directory (`mkdir -p backend/app`) and create a file called `server.js` (`touch backend/app/server.js`).

Open `backend/app/server.js` and add the following:

```javascript
const express = require('express'); // Load express framework
const app = express();              // Initialize express app

const DEFAULT_PORT = 3000; 

// Define behavior for the server when it receives a request with this URL
app.get('/', function (req, res) {
  res.send('Hello World!');
});

// Start server by listening to designated port and responding to all requests
const server = app.listen(process.env.PORT || DEFAULT_PORT, function () {
  // Log a message to indicate that the server was started correctly
  const port = server.address().port;
  console.log(`Server listening on port ${port}!`);
});
```

|---
| ![Pause Point]({{site.baseurl}}/assets/general/pause_point.png) | [What is asynchronous code execution?]({{site.baseurl}}/explanations/asynchronous-code.html) |

Start the server by running `node backend/app/server.js`:

```bash
~/projects/hello-world (master) $ node backend/app/server.js
Server listening on port 3000!
```

### Send a request to the server

We can test our server by sending it a request. The address for our local server is `http://localhost:3000`, since we've defined the port to use as `3000`.

If we open our browser and navigate to `http://localhost:3000`, that will send a GET request to our server for URL `/`. Our browser will try to render whatever the server sends back. So we should see something like this:

![Server Response in Browser]({{site.baseurl}}/assets/web-app/screenshot_server-hello-world.png) 

Alternatively, we can use the command line to send a request directly to the server using the [curl](https://curl.haxx.se/) tool.

`curl http://localhost:3000/` also sends a GET request to our server and prints the result to our shell.

```bash
~/projects/hello-world $ curl http://localhost:3000/
Hello World!
```

### Restart the server whenever any changes are made

Unlike our Ember server, we need to restart the Express server every time we make a change. Instead of manually restarting, we can use [nodemon](https://nodemon.io/) to watch our files and restart the backend server for us whenever we make changes.

`npm install nodemon --save-dev`

We want to `--save-dev` instead of `--save` to indicate that this is only a dependency for developing new code in our app — we won't need `nodemon` to run when we deploy, since we won't be making changes.

Once nodemon is installed, we can quit our old Express server and restart it using nodemon:

`$(npm bin)/nodemon backend/app/server.js`

We use `$(npm bin)/` here to ensure that the version of `nodemon` that we're running is the one that we just installed in this project. You can also install nodemon globally if you'd prefer to use it directly: `npm install -g nodemon`.

You can tell that nodemon started correctly if it outputs something like this:

```bash
~/projects/hello-world $ $(npm bin)/nodemon backend/app/server.js
[nodemon] 1.11.0
[nodemon] to restart at any time, enter `rs`
[nodemon] watching: *.*
[nodemon] starting `node backend/app/server.js`
Server listening on port 3000!
```

Once that's running, we should be able to keep making changes and have the server automatically restart for us.

### Proxy from the Ember app to the server

Now we have two servers running — one for our Ember app and one for our Express server. But how can we send requests from our Ember app to our server?

We can proxy all requests made from our Ember app to a given address. We'll want to restart our Ember server with the `--proxy` option.

`ember serve --proxy http://localhost:3000`

We should now expect that all requests we make to `http://localhost:4200` should be served by `http://localhost:3000` — but what if the Express server and the Ember server define the same behavior for the same URL?

That's currently true for our `/` (index) route. Our Express server returns `Hello World!`:

```bash
~/projects/hello-world (master) $ curl http://localhost:3000/
Hello World!
```

But our Ember server doesn't proxy that request to the Express server, it just returns the HTML for its own index page:

```bash
~/projects/hello-world (master) $ curl http://localhost:4200/
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>HelloWorld</title>
    <meta name="description" content="">
    <meta name="viewport" content="width=device-width, initial-scale=1">


<meta name="hello-world/config/environment" content="%7B%22modulePrefix%22%3A%22hello-world%22%2C%22environment%22%3A%22development%22%2C%22rootURL%22%3A%22/%22%2C%22locationType%22%3A%22auto%22%2C%22EmberENV%22%3A%7B%22FEATURES%22%3A%7B%7D%2C%22EXTEND_PROTOTYPES%22%3A%7B%22Date%22%3Afalse%7D%7D%2C%22APP%22%3A%7B%22name%22%3A%22hello-world%22%2C%22version%22%3A%220.0.0+b65ae851%22%7D%2C%22exportApplicationGlobal%22%3Atrue%7D" />
<script src="/ember-cli-live-reload.js" type="text/javascript"></script>

    <link rel="stylesheet" href="/assets/vendor.css">
    <link rel="stylesheet" href="/assets/hello-world.css">


  </head>
  <body>


    <script src="/assets/vendor.js"></script>
    <script src="/assets/hello-world.js"></script>


  </body>
</html>
```

### Namespace all server requests

Although we set up the proxy correctly, we need to namespace all our server requests so that Ember doesn't try to route them through its own application router.

Let's preface all the endpoints in our backend server with `api`.

We should modify `backend/app/server.js` first:

```javascript
// Define behavior for the server when it receives a request with this URL
app.get('/api', function (req, res) {
  res.send('Hello World!');
});
```

Nodemon should automatically restart the Express server when we save that file, so we should see the following output with our curl requests:

```bash
~/projects/hello-world $ curl http://localhost:3000/
Cannot GET /
~/projects/hello-world $ curl http://localhost:3000/api
Hello World!
```

To prove that our proxying is working correctly, we can send our request to the Ember port (`4200`) instead of our Express port (`3000`) and still get the same result:

```bash
~/projects/hello-world $ curl http://localhost:4200/api
Hello World!
```

**Note:** There is nothing special about `api/` as a namespace, other than convention. The only thing that matters in terms of proxying is that we cannot define an Ember route with that same URL.

### Return a JSON object from the server

We're now correctly proxying from Ember to our Express server, but the response isn't terribly exciting. Let's add another endpoint that returns a JSON object with a greeting based on query params.

Add the following to `backend/app/server.js` (right below the definition for `/api`):

```javascript
app.get('/api/greeting', function (req, res) {
  const greeting = req.query.name !== undefined ?
    `Hello ${req.query.name}!` :
    `Hello stranger!`;

  res.send({ greeting });
});
```

Let's send a request to our new endpoint, without providing any query params:

```bash
~/projects/hello-world (master) $ curl http://localhost:4200/api/greeting
{"greeting":"Hello stranger!"}
```

Now if we provide a name via query params, we should see a different response:

```bash
~/projects/hello-world $ curl http://localhost:4200/api/greeting?name=Marie
{"greeting":"Hello Marie!"}
```

If you aren't seeing this new route, you may need to verify that you've set up nodemon correctly, or manually restart the Express server.

---

## Review

You installed Express and created a backend server.

You installed nodemon to automatically restart the Express server whenever you make changes.

You proxied requests from the Ember server to the Express server.

You sent requests to the Express and Ember servers via curl.

**[Proceed to the next step.](step5.html)**
