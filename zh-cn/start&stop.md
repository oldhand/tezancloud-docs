## centos与mac下启动
  * 首先确保redis服务端已经启动
  * 启动消息队列
  ```bash
  cd rabbitmq
  ./rabbitmq.sh start
  ```
  * 启动tezancloud
  ```bash
  ./tezancloud.sh start #以后台的模式启动
  ./tezancloud.sh live  #以在线控制台的模式启动 显示平台访问信息
  ./tezancloud.sh debug #以debug模式启动 显示出错信息，方便调试
  ./tezancloud.sh stop #停止后台模式
  ```
  * 启动消息队列响应端
  ```bash
  cd mqc
  ./mqc.sh start #以后台的模式启动
  ./mqc.sh debug #以debug模式启动
  ./mqc.sh stop #停止后台模式
  ```
  
  * 特殊命令
  ```bash
  ./date.sh  #从时间服务器，校准本地时间
  ./createdb.sh   #建立空数据库，当导入数据时，需要预先建立空的数据库
  ./stop.sh   #平台启动会自动启动PostgreSQL,但停止时不会自动停止，此命令用来停止PostgreSQL
  ```
## windows下启动
  安装[wzarp](https://github.com/oldhand/wzarp)后
  运行run.bat即可