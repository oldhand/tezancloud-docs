**当远程访问平台时，REST必须通过token认证**<br>
**本机访问，或内网访问时，无需token认证**
## 配置Token认证码
在安装目录，可以找到./deps/store/store.conf的配置文件。
```bash
{'token',"****************"}.

```
请配置token认证码。

 
## Token认证算法
 
Token认证算法，实质是就是MD5算法，
```bash
token = MD5(相对请求地址 + token认证码 + 时间戳);

```


## 如何认证？
实例简述：<br>
实际URL请求为：localhost:8000/xn/rest/1.0/content(id=284436)?xn_out=xml<br>
相对请求地址为：/xn/rest/1.0/content(id=284436)?xn_out=xml<br>
```bash
var timestamp = ?;
var token = md5("/xn/rest/1.0/content(id=284436)?xn_out=xml" + "****************" + timestamp);

```
timestamp为时间戳。<br>
将{"token",token,"timestamp":timestamp} 放入请求头即可。<br>

## 注意保护你的Token认证码
当你的Token认证码被泄露后，就存在请求被模拟的可能。