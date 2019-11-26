**Credential 即访问票据，为接口加密服务，确保您的数据传输的安全**<br>
**当远程访问平台时，REST必须获得Credential**<br>
**本机访问，或内网访问时，无需Credential**

## 配置公钥与私钥
平台使用RSA加密算法，确保接口传输过程的数据安全。
在./deps/store/目录下，有公钥与私钥两个文件。
```bash
private_key.pem //私钥
public_key.pem //公钥

```
如何生成公钥与私钥，请自行搜索相关文档。<br>
**当您更改了上述两个文件后，平台的开发者也无法解密您的数据。**



## 如何获得Credential？
实例简述：<br>
```bash
var timestamp = ?; //时间戳
var appid = ?; //每一个项目共用一个appid，自定义
var token = ?  //token认证码
var uniqueid = ?; //设备ID
var secret = md5(appid + uniqueid + timestamp + token);
var url = '/xn/rest/1.0/credential(appid=$appid&secret=$secret&uniqueid=$uniqueid&timestamp=$timestamp)";
```
调用此请求可以获得加密的Credential。<br>
使用RSA可以解密，获得正确的Credential。<br>

## 如何使用Credential？
正确的Credential，包含access_token，public_key， 二个数据字段。<br>
access_token为当前票据的key，<br>
public_key为当前票据的公钥，每一个设备在获得票据后，是独立的公钥与私钥。<br>
Credential的有效期时间为2小时。<br>
将{"accesstoken",access_token} 放入请求头即可。
## 加解密算法
数据传输过程中，服务端首先使用了gzip进行压缩处理，然后使用RSA进行加密，最后base64。<br>
客户端解密，首先进行base64解密，然后RSA进行解密处理，最后gzip解压缩，还原数据。

## 注意保护你的公钥与私钥
当你的Token认证码被泄露后，传输的数据就也可能泄露。服务器的数据就存在被篡改的可能。