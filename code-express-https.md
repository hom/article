## Node.js配合Express搭建HTTPS服务器
1. 在项目目录中新建`ssl`目录，生成`SSL`秘钥
```bash
$ openssl genrsa -out yourkey.pem 1024
$ openssl req -new -key yourkey.pem -out yourcsr.csr
$ openssl x509 -req -in yourcsr.csr -signkey yourkey.pem -out yourcert.cert
```
如果已经存在，需确保格式为`.pem`
```bash
$ openssl x509 -in yourkey.crt -out yourkey.pem -outform PEM
$ openssl x509 -in yourcert.crt -out yourcert.cert -outform PEM
```

2. 在项目中新建`ssl-license.js`
```js
let fs = require('fs');

// ssl license
let hskey = fs.readFileSync('ssl/yourkey.pem');
let hscert = fs.readFileSync('ssl/yourcert.cert');

let ssl = {
  key: hskey,
  cert: hscert
};

module.exports = ssl;
```

3. 在项目启动文件中添加
```js
let express = require("express");
let ssl = require("./ssl-license");
let https = require("https");

let app = express();

let httpsServer = https.createServer(ssl,app).listen(3000, () => {
  console.log("node is running")
})

```