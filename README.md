# Welcome to Keeling Js

Keeling Js is a fast and light weight NodeJs server based on ExpressJs. On the contrary to specifically writing router and resolver, Keeling Js provides stable router manipulation based on file structures, so that you don't have to write so many back end control files.

Its installation is very fast and easy. In any empty directory, simply use

```
$ cd <YOUR_DIRECTORY>
$ npm init
```

to initiate a new NPM repository \(for NPM documentation please go to [https://www.npmjs.com](https://www.npmjs.com)\) by following all the prompts in the command line, and then

```
$ npm install keeling-js
```

to install keeling-js to your NodeJs application. After the installation, you can see many directories been added inside you directory. Now, except there's "nothing" inside this repository, this NodeJs Application is actually well-functioning! You can now just start this NodeJs server by typing

```
$ npm start
```

directly. Now if you see a line like

```
Successfully started server Keeling Js Default in port 21023
```

then the installation is successful and you can now access [http://localhost:21023/](http://localhost:21023/) in your browser! \(Though you might see 404 after that since your requested main page does not exist\).

Let's dive deeper to see how these directories going to be look like and how to config the whole server with Keeling Js.

* [Configuration](/configuration.md)
* [Server Setup](/server-creation.md)
* [Html & Static Router](/methods.md)
* [Ajax Handler](/ajax-request.md)
* [Scheduled Tasks](/scheduled-events.md)

There are also submodules that you can use \(still updating\):

* Debug
* Crypto
* Image



