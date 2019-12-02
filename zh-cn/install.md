

## centos下安装
  
  ```bash
  yum -y install gcc
  yum -y install ncurses-devel
  yum -y install readline-devel
  yum -y install openssl-devel
  yum -y install zlib-devel
  yum -y install wget
  # 安装redis
  yum -y install redis  
  # 安装erlang 经测试，erlang版本必须不低于20.3。 
  wget http://erlang.org/download/otp_src_20.3.tar.gz
  tar xzvf otp_src_20.3.tar.gz  
	cd otp_src_20.3
	./configure
	make 
	make install
  # 安装PostgreSQL 建议10.4版本。
  wget https://ftp.postgresql.org/pub/source/v10.4/postgresql-10.4.tar.gz
  tar xzvf postgresql-10.4.tar.gz  
	cd postgresql-10.4
	./configure
	make  
	make install
  ```
  若需要使用图片CDN, 则需要安装ImageMagick
  ```bash
  yum install ImageMagick
  ```

## mac苹果系统下安装
 首先需要安装brew
 ```bash
 /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
 ```
 ```bash
  # 安装redis
  brew install redis  
  # 安装erlang 经测试，erlang版本必须不低于20.3。 
  wget http://erlang.org/download/otp_src_20.3.tar.gz
  tar xzvf otp_src_20.3.tar.gz  
	cd otp_src_20.3
	./configure
	make 
	make install
  # 安装PostgreSQL 建议10.4版本。
  wget https://ftp.postgresql.org/pub/source/v10.4/postgresql-10.4.tar.gz
  tar xzvf postgresql-10.4.tar.gz  
	cd postgresql-10.4
	./configure
	make  
	make install
 ```

  若需要使用图片CDN, 则需要安装ImageMagick
  ```bash
  brew install imagemagick@6
  ```
 
## windows下安装
   首先需要安装[wzarp](https://github.com/oldhand/wzarp)集成开发环境，可以大大减少你的安装配置的工作量。<br>
   安装集成环境后，下载[tezancloud](https://github.com/oldhand/tezancloud)到安装目录
   ```bash
   cd wzarp 
   git clone https://github.com/oldhand/tezancloud.git
   ```


