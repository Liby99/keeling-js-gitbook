# Ajax Handler

Keeling Js has a well wrapped Ajax Handler system. Let's start from the **front-end**.

### Front-end

All the requests that send to the ajax handler will have a prefix of the **ajax directory** that you specified in the config \(which, by default is `/ajax` \). Let's say you have `/ajax` , then an Ajax Request will look like this:

```
/ajax/<HANDLER>?action=<ACTION>
```

As you can see the request has two main variables. The first one is `<HANDLER>` and the second is `<ACTION>` . These are two credentials to locate the handler and action. Let's start from handler.

### Back-end Handler

All back-end handler are `.js` files located inside `ajax/` directory \(or the one you specified in your config file\). If we now have an Ajax request

```
/ajax/user?action=add_user
```

Keeling Js will go to find the `ajax/user.js` and require it. There could also be more path inside the request

```
/ajax/admin/user?action=add_admin
```

Keeling Js will go to find the `ajax/admin/user.js` .

Now let's take a look at what a handler will look like:

```js
// ajax/user.js
module.exports = {
    add_user: function (req, res) {
        if (req.body.username && req.body.username === "") {
            //....
            res.success({
                username: req.body.username
            });
        }
        else {
            res.error(1, "no username specified");
        }
    },
    remove_user: function (req, res) {
        res.formatResponse(1000, "error with return content", {
            removed_user: "john doe"
        });
    }
}
```

In this specific example, `add_user` and `remove_user` will be two of the **actions** under `user` handler. And action must be **function** with two parameters `req` and `res` . Since KeelingJs use [body-parser](#), [express-session](#), and [cookie-parser](#), you can use all the APIs offered by these three libraries in `req` and `res` . But as always, we provide several new functions with response so that you can better handle the Ajax requests.

#### res.success\(object\)

* object: &lt;object&gt;, the content you want to return to the user. Better be an object for front-end wrapping

Pass in an object as return value to response the user. The user will receive a JSON response look like this:

```js
{
    "code": 0,
    "msg": "",
    "content": <object>
}
```

#### res.error\(code, msg\)

* code: &lt;number&gt;, the error code of the error. Better not be 0 since 0 is already used by `success`
* msg: &lt;string&gt;, the string message to return to the user

Pass in error code and error message to send such JSON response to the user:

```js
{
    "code": <code>,
    "msg": <msg>,
    "content": {}
}
```

#### res.formatResponse\(code, msg, object\)

* code: &lt;number&gt;, the error code of the error. Better not be 0 since 0 is already used by `success`
* msg: &lt;string&gt;, the string message to return to the user
* object: &lt;object&gt;, the content you want to return to the user. Better be an object for front-end wrapping

A wrapper of `success` and `error` methods. This time you can manipulate all three parameters in this formatted JSON object

```js
{
    "code": <code>,
    "msg": <msg>,
    "content": <object>
}
```
