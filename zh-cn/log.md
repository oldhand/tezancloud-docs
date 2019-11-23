

## 日志说明
  
  ```bash
  [debug][127.0.0.1][0/30][1ms][GET][admin]:/xn/rest/1.0/content(type eic 'users'&my.profileid = 'm0ju5li2541')?count=true&xn_out=xml&from=0&to=-1&order=my.sequence@A_N
  ```
  * [debug] : 日志级别
  * [127.0.0.1] :  访问IP
  * [0/30] : 占用连接池数/总连接池数
  * [1ms] : 当次请求后台总计执行时间
  * [GET] : GET表示请求类型(get表示查询数据，POST为创建数据，PUT为修改数据，DELETE为删除数据)
  * [admin] : 请求的应用名称
  * /xn/rest/1.0/content(type eic 'users'&my.profileid = 'm0ju5li2541') : 请求的主体，综合查询条件
  * count=true : 是否返回记录总数
  * xn_out=xml : 数据格式(xml,json,binary)
  * from=0 : 数据分段起始位置，默认0
  * to=-1 : 数据分段结束位置，默认100，为-1时表示不分页，返回全部数据
  * order=my.sequence@A_N : 排序，支持多字段排序，(A表示升序,D表示降序,A_N表示数字升序,D_N表示数字降序)
  
  ```bash
  [debug]clear memcache Label: "loginhistorys,loginhistorys_m0ju5li2541" Hostname:"admin"
  ```
  
  ```bash
  memcache_set key: "dz6uhkliy1a7zygp1d3ktxi2d" Label: "announcements" stored 
  ```

## log4erl.conf 配置说明
  
  ```bash
  logger{
   %	file_appender app2{
   %		dir = "./logs",
   %		level = all,
   %		file = tezan,
   %		type = size,
   %		max = 8192000, 
   %		suffix = log,
   %		rotation = 1,
   %		format = '[%L] [%j %t] %l%n'
   %	}

  	console_appender app1{
  		level = debug,
  		%%format = '%T %j [%L] %l%n'
  		format = '[%L]%l%n'

  	}
  }
  ```
  默认关闭日志的文件存储；<br>
  当需要调试，或查找错误信息时，可以打开文件存储，去掉%即可。<br>
  >注意，实测结果显示，线上环境最好关闭日志的文件存储，这样前台访问的效率可以达到最高。<br>

