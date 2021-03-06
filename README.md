# `express-http-to-https`

express-http-to-https is a node.js package for providing an Express middleware that redirects the client to HTTPS if they attempt to connect over HTTP.

## Installation
`$ npm install --save express-http-to-https`


## Usage

`app.use(redirectToHTTPS(ignoreHosts, ignoreRoutes);`


### Configuration Options

* __ignoreHosts__: An array of strings of the hostnames on which to not enable the redirect. _note:_ you must include the port here, for example `[/localhost:8080/]`.
* __ignoreRoutes__: An array of strings of the routes on which not to enable the redirect.
* __redirectCode__: The HTTP status code to return when redirecting. Defaults to 302 "found" can be any status code


### Example

````js
var express = require('express');
var app = express();

var redirectToHTTPS = require('express-http-to-https').redirectToHTTPS

// Don't redirect if the hostname is `localhost:port` or the route is `/insecure`
app.use(redirectToHTTPS([/localhost:(\d{4})/], [/\/insecure/], 301));

app.get('/', function (req, res) {
  res.send('Hello World!');
});

app.get('/insecure', function (req, res) {
  res.send('Dangerous!');
});

app.listen(3000, function () {
  console.log('Example app listening on port 3000!');
});

app.listen(8080, function () {
  console.log('Example app listening on port 8080 insecurely!');
});
````

[![JavaScript Style Guide](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)

## License
MIT License

## Author
Max Walker (max@maxwalker.me)

## Contributors
Aleksander Szmigiel
