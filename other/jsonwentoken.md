# 目录

- [jsonwebtoken](#jsonwebtoken)

## jsonwebtoken

```
  var JWT = require('jsonwebtoken');

  exports.generateToken = function(key){
    var payload = key || Date.now();
    return JWT.sign(payload,Date.now() + "")
  }

  var aa = this.generateToken()
  console.log('aa',aa)
```
