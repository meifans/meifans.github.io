
## 破解

### mac

1. 从官网安装 http://staruml.io/
2. 编辑 /Applications/StarUML.app/Contents/www/license/node/LicenseManagerDomain.js
3. 编辑 这个函数 function validate(PK, name, product, licenseKey)， 让它返回如下代码
````
return {
           name: "meifans", //自定义名字
           product: "StarUML",
           licenseType: "vip",
           quantity: "mergades.com",
           licenseKey: "My Heart Will Go On" //自定义秘钥
       };
````
4. help>enter license 输入上面的名字和秘钥
