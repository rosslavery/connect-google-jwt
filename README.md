Use Google's JWTs to authenticate calls to your backend API.

Google implements the standard OpenID Connect, after the authorization flow with `response_type=id_token` you will get a JWT in the client side of your application. You can use this JWT to authenticate calls to your api.

This middleware validate three things __expiration__, __audience__ and __signature__.

The signature is validated with the certs from https://www.googleapis.com/oauth2/v1/certs as stated in Google Docs [Validating an ID Token](https://developers.google.com/accounts/docs/OAuth2Login#validatinganidtoken). These certs are downloaded when your application starts and every 24hs.

If you want to validate JWT's from other sources (not google) use [express-jwt](http://github.com/auth0/express-jwt).

## Install

~~~
$ npm i connect-google-jwt
~~~

## Usage

In an express.js application:

~~~javascript
var googleJWT = require('connect-google-jwt');

app.configure(function () {
  //middlewares
  this.use('/api', googleJWT({
    client_id: 'your client id'
  }))
});

app.get('/api/messages', function (req, res) {
  req.user // you have the decoded JWT here
});
~~~

## Issue Reporting

If you have found a bug or if you have a feature request, please report them at this repository issues section. Please do not report security vulnerabilities on the public GitHub issue tracker. The [Responsible Disclosure Program](https://auth0.com/whitehat) details the procedure for disclosing security issues.

## License

The MIT License (MIT)

Copyright (c) 2014 AUTH10 LLC

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
