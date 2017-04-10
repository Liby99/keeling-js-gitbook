# Server Creation

### Default Server Setup

When using this setup, you don't need to write any server entry point scripts. Just use

```
$ npm start
```

in the command line will start the server with the config file you specified in `data/config.json` .

As you might notice the starting point of the server is not specified by yourself. So you might want to add an `index.js` and modify the `package.json`'s starting script yourself. Here is how you are going to do it.

### Basic Server Setup

First create a file in the application root directory called `index.js` and paste these codes into it:

```js
// index.js
var keeling = require("keeling-js");
var server = keeling.createServer();
server.start();
```

This does exactly the same thing as the default starting script do. Since there's nothing specified in `keeling.createServer()` then it will by default use your config file `data/config.json` .

Now you want to change the `package.json` to fit your new `index.js` :

```js
// package.json
{
    ...
    "scripts": {
        ...
        "start": "node index.js"
    },
    ...
}
```

So that next time you type `npm start` it will use `node index.js` to run your own application starting point.

### Specify Server Config in Code

If you do not want to put a `config.json` under `data/` then it is totally fine. If you do just as above, it will use the default config, which might not be all the thing you want. But we also provide another possibility, which is to specify the config inside your server creation. Then your `index.js` will look like this:

```js
// index.js
var config = {
    name: "My App"
    port: 8192
}

var keeling = require("keeling-js");
var server = keeling.createServer(config); // <- PASS A CONFIG OBJECT
server.start();
```

Here you can see we passed a config object into the createServer function. By doing so, the server will not try to refer to the actual config file `data/config.json` but only this config you wrote here. Of course any missing entry will be filled with default value.

### Starting Multiple Servers in the Same Starting Script

Seeing the previous example you must be wondering if we can create multiple servers. The answer is, **YES!** So here is how you are going to do it:

```js
// index.js
var keeling = require("keeling-js");

var userServer = keeling.createServer({
    name: "My App - User",
    port: 8192,
    public_directory: "user_public"
});
userServer.start();

var adminServer = keeling.createServer({
    name: "My App - Admin",
    port: 8193,
    public_directory: "admin_public"
});
adminServer.start();
```

In this example we started two servers and they will listen to different ports and serve different static files \(one from `user_public` directory and the other from `admin_public`\). And in this specific example they will share the same Ajax Handlers.
