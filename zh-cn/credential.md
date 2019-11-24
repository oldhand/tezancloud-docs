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
实际URL请求为：localhost:8000/xn/rest/1.0/content(id=284436)?xn_out=xml<br>
相对请求地址为：/xn/rest/1.0/content(id=284436)?xn_out=xml<br>
```bash
var timestamp = ?;
var token = md5("/xn/rest/1.0/content(id=284436)?xn_out=xml" + "****************" + timestamp);

```
timestamp为时间戳。<br>
将{"token",token,"timestamp":timestamp} 放入请求头即可。<br>


## 如何使用Credential？

## 注意事项

## 注意保护你的公钥与私钥
当你的Token认证码被泄露后，传输的数据就也可能泄露。服务器的数据就存在被篡改的可能。