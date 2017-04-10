# Html & Static Router

### Html

This is the part where keeling-js getting very handy. Keeling Js will help you build up a connection between your `.html` files and the `.js` handlers that provide information to render the `.html` files.

Before everything is said, Keeling Js uses EJS as its default renderer. The full documentation of this Effective JavaScript templating is in its own website [http://ejs.co](http://ejs.co).

Every `.html` file in your specified **public directory** \(`/public` by default\) will be rendered by EJS. So you can easily separate views from HTML files. Like create a `navbar` view for all the pages that needs a `navbar` so that you don't have to copy and paste the code multiple times. If there's nothing EJS in the `.html` file, then the static version will be delivered to the user. If the file does not exist, then Keeling Js will redirect the request to the error page, which we will elaborate on [here](#error).

Of course, EJS as a powerful renderer doesn't only handle the static files. You can pass in actual data to the `.html` files by using router. Let's step in.

### Router

All router files must be stored in your specified **router directory **\(`/router` by default\). And every router file will have an one to one relation to a `.html` file with **exactly the same name and path** in the **public directory **\(though it's not a _must_ if you know what you are doing\). Let's say if you have `public/index.html` and you want a router to provide data to render this page, you want to have a `router/index.js` in the router directory. If you have `public/admin/dashboard.html` then the corresponding router will be `router/admin/dashboard.js` .

Let's see what the router will look like:

```js
// router/index.js
module.exports = function (req, res, callback) {
    callback({
        "message": "Hello World"
    });
};
```

A router will be a **function** that takes three arguments. `req` \(request\), `res` \(response\), and `callback` , a callback function used to pass back the data. As you can see we passed an object to the callback function including a `message` of `Hello World` . Now that if we have a `public/index.html` that is

```
<!-- public/index.html -->
<html>
    <head></head>
    <body>
        <%= message %>
    </body>
</html>
```

then the result html will be rendered as

```
<!-- rendered public/index.html -->
<html>
    <head></head>
    <body>
        Hello World
    </body>
</html>
```

Of course this is the very basic use of router, and you can manipulate the `req` and `res` as much as you can by referring to [ExpressJs' documentation](http://expressjs.com/), such as `req.query` and `res.send("...")` \(note: don't call callback again if you have already called `res.send("...")` \). Keeling Js also uses [body-parser](https://github.com/expressjs/body-parser), [express-session](https://github.com/expressjs/session), and [cookie-parser](https://github.com/expressjs/cookie-parser), so please refer to these documentations when using them.

There's another thing that is very useful:

##### res.error\(&lt;code&gt;, &lt;msg&gt;\)

This will redirect the response to the **error\_page** specified in the config with the query params `code` and `msg` .

### Error Page {#error}

Error page is the `error_page` that specifies in the [config](/configuration.md). So if you have `error` in config then the actual error file should be `public/error.html` . In this case, when `res.error(<code>, <msg>)` is called, the request will be redirected to such web page:

```
/error.html?code=<code>&msg=<msg>
```

If you do not have an `error.html` that's ok, since Keeling Js will still give the user the information. But you can definitely make your error page more beautiful by writing an `error.html` and also its router `error.js` .

Keeling Js will by default redirect every error to the Error Page. Like if your `.html` file is not found, then it will send a 404 error; if your page router is catching error, then it will send a 500 error.

### Static Files

Every file in the **public directory** other than `.html` files will be considered as **static file**. The static files will be send to the user **as is**.
