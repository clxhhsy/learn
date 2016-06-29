# nginx安装
	nginx先决条件
	g++、gcc、openssl-devel、pcre-devel、zlib-devel

### 步骤一、下载nginx
[nginx官网](http://nginx.org)
下载完成后上传至服务器/usr/local目录下

### 步骤二、安装nginx先决条件
因为笔者所用系统为centos，所以这里采用yum安装

	yum -y install gcc-c++ zlib-devel openssl-devel pcre-devel

### 步骤三、安装nginx
	#1. 进入nginx安装包目录
	cd /usr/local
	#2. 解压nginx安装包
	tar -zxvf nginx-1.10.1.tar.gz
	#3. 进入解压目录
	cd nginx-1.10.1
	#4. 生成make文件，并指定安装目录
	./configure --prefix=/usr/local/nginx
	#5. 编译
	make
	#6. 安装
	make install

	到此安装过程结束，可进入/usr/local/nginx/sbin目录下启动nginx
	