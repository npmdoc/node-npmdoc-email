# api documentation for  [email (v0.2.6)](https://github.com/aheckmann/node-email#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-email.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-email) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-email.svg)](https://travis-ci.org/npmdoc/node-npmdoc-email)
#### A simple wrapper for sendmail.

[![NPM](https://nodei.co/npm/email.png?downloads=true)](https://www.npmjs.com/package/email)

[![apidoc](https://npmdoc.github.io/node-npmdoc-email/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-email_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-email/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-email/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-email/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Aaron Heckmann",
        "email": "aaron.heckmann+github@gmail.com"
    },
    "bugs": {
        "url": "http://github.com/aheckmann/node-email/issues"
    },
    "dependencies": {},
    "description": "A simple wrapper for sendmail.",
    "devDependencies": {
        "gleak": "0.4.0"
    },
    "directories": {},
    "dist": {
        "shasum": "96c538cf4a8a23db8bd2af7156c7b968f39abc4c",
        "tarball": "https://registry.npmjs.org/email/-/email-0.2.6.tgz"
    },
    "engines": {
        "node": ">= 0.1.92"
    },
    "homepage": "https://github.com/aheckmann/node-email#readme",
    "keywords": [
        "email",
        "sendmail",
        "node-email"
    ],
    "licenses": [
        {
            "type": "MIT",
            "url": "http://www.opensource.org/licenses/mit-license.php"
        }
    ],
    "main": "./index",
    "maintainers": [
        {
            "name": "aaron",
            "email": "aaron.heckmann+github@gmail.com"
        }
    ],
    "name": "email",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/aheckmann/node-email.git"
    },
    "version": "0.2.6"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module email](#apidoc.module.email)
1.  [function <span class="apidocSignatureSpan">email.</span>Email (config)](#apidoc.element.email.Email)
1.  [function <span class="apidocSignatureSpan">email.</span>isValidAddress (rawAddress)](#apidoc.element.email.isValidAddress)
1.  number <span class="apidocSignatureSpan">email.</span>timeout
1.  object <span class="apidocSignatureSpan">email.</span>Email.prototype
1.  string <span class="apidocSignatureSpan">email.</span>version

#### [module email.Email](#apidoc.module.email.Email)
1.  [function <span class="apidocSignatureSpan">email.</span>Email (config)](#apidoc.element.email.Email.Email)

#### [module email.Email.prototype](#apidoc.module.email.Email.prototype)
1.  [function <span class="apidocSignatureSpan">email.Email.prototype.</span>send (callback)](#apidoc.element.email.Email.prototype.send)
1.  [function <span class="apidocSignatureSpan">email.Email.prototype.</span>valid (callback)](#apidoc.element.email.Email.prototype.valid)
1.  object <span class="apidocSignatureSpan">email.Email.prototype.</span>options
1.  string <span class="apidocSignatureSpan">email.Email.prototype.</span>msg



# <a name="apidoc.module.email"></a>[module email](#apidoc.module.email)

#### <a name="apidoc.element.email.Email"></a>[function <span class="apidocSignatureSpan">email.</span>Email (config)](#apidoc.element.email.Email)
- description and source-code
```javascript
function Email(config) {
  config = config || {};

  ; ['to'
    ,'from'
    ,'cc'
    ,'bcc'
    ,'replyTo'
    ,'subject'
    ,'body'
    ,'bodyType'
    ,'altText'
    ,'timeout' ].forEach(function (key) {
    this[key] = config[key];
  }, this);

  this.path = config.path || "sendmail";
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.email.isValidAddress"></a>[function <span class="apidocSignatureSpan">email.</span>isValidAddress (rawAddress)](#apidoc.element.email.isValidAddress)
- description and source-code
```javascript
function isValidAddress(rawAddress) {
  // john smith <email@domain.com> | email@domain.com
  var address = capturergx.exec(rawAddress);
  return address && address[1]
    ? emailrgx.test(address[1])
    : emailrgx.test(rawAddress);
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.email.Email"></a>[module email.Email](#apidoc.module.email.Email)

#### <a name="apidoc.element.email.Email.Email"></a>[function <span class="apidocSignatureSpan">email.</span>Email (config)](#apidoc.element.email.Email.Email)
- description and source-code
```javascript
function Email(config) {
  config = config || {};

  ; ['to'
    ,'from'
    ,'cc'
    ,'bcc'
    ,'replyTo'
    ,'subject'
    ,'body'
    ,'bodyType'
    ,'altText'
    ,'timeout' ].forEach(function (key) {
    this[key] = config[key];
  }, this);

  this.path = config.path || "sendmail";
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.email.Email.prototype"></a>[module email.Email.prototype](#apidoc.module.email.Email.prototype)

#### <a name="apidoc.element.email.Email.prototype.send"></a>[function <span class="apidocSignatureSpan">email.Email.prototype.</span>send (callback)](#apidoc.element.email.Email.prototype.send)
- description and source-code
```javascript
send = function (callback) {
  if (!this.valid(callback)) return;
  var sendmail = spawn(this.path, ['-i', '-t'], this.options);
  sendmail.on('exit', function(code) {
    var err = null;
    if (code !== 0) {
      err = new Error("Sendmail exited with code: " + code);
    }

    if (callback) {
      callback(err);
    }
  });

  sendmail.stdin.end(this.msg);
}
```
- example usage
```shell
...
, to:   "you@example.com"
, subject: "Knock knock..."
, body: "Who's there?"
})

// if callback is provided, errors will be passed into it
// else errors will be thrown
myMsg.send(function(err){ ... })

In this example we set the global 'from' property so that all
email is sent from the same address.

var lib = require('path/to/email')
  , Email = lib.Email;
...
```

#### <a name="apidoc.element.email.Email.prototype.valid"></a>[function <span class="apidocSignatureSpan">email.Email.prototype.</span>valid (callback)](#apidoc.element.email.Email.prototype.valid)
- description and source-code
```javascript
valid = function (callback) {
  if (!requiredFieldsExist(this, callback)) return false;
  if (!fieldsAreClean(this, callback)) return false;

  var validatedHeaders = ['to','from','cc','bcc','replyTo']
    , len = validatedHeaders.length
    , self = this
    , addresses
    , addLen
    , key;

  while (len--) {
    key = validatedHeaders[len];
    if (self[key]) {
      addresses = toArray(self[key]);
      addLen = addresses.length;
      while (addLen--) {
        if (!isValidAddress(addresses[addLen])) {
          return error("invalid email address : " + addresses[addLen], callback);
        }
      }
    }
  }

  return true;
}
```
- example usage
```shell
...
this.path = config.path || "sendmail";
}


Email.prototype = {

send: function (callback) {
  if (!this.valid(callback)) return;
  var sendmail = spawn(this.path, ['-i', '-t'], this.options);
  sendmail.on('exit', function(code) {
    var err = null;
    if (code !== 0) {
      err = new Error("Sendmail exited with code: " + code);
    }
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
