# Kong使用MySQL

Kong默认支持的数据库包括PostgreSQL和Cassandra，在实际使用中，很多用户都是MySQL重度用户。针对这些用户，我们开发了MySQL DAO。目前已经验证和测试过的环境是CentOS7+MySQL5.7+或者CentOs7+Mariadb10+。

这里是下载链接：[kong-0.14.1-51.el7_pl.x86_64.rpm](http://www.polaristech.io/assets/kong-0.14.1-51.el7_pl.x86_64.rpm) MD5为9740c60baf57d17f1aceecb1800d7a1e

## 安装步骤

- 首先需要一个可以访问的MySQL实例，假设在localhost:3306，用户是root，密码是kong，数据库是kong。
- 添加epel的repo。安装有些依赖来自epel。
~~~
yum -y install epel-release
~~~
- 本地安装下载的文件
~~~
yum -y localinstall kong-0.14.1-51.el7_pl.x86_64.rpm
~~~

## 配置和使用

- 默认的配置文件在/etc/kong/kong
~~~
cp /etc/kong/kong.conf.default /etc/kong/kong.conf
~~~

- 编辑其中的MySQL配置部分，默认在325-335行
~~~
325 database = mysql               # Determines which of PostgreSQL or Cassandra
326                                  # this node will use as its datastore.
327                                  # Accepted values are `postgres` and
328                                  # `cassandra`.
329 
330 mysql_host = 127.0.0.1             # The PostgreSQL host to connect to.
331 mysql_port = 3306                  # The port to connect to.
332 mysql_user = root                  # The username to authenticate if required.
333 mysql_password = kong                  # The password to authenticate if required.
334 mysql_database = kong              # The database name to connect to.
~~~

- 执行kong migrations up
~~~
kong migrations up
~~~

- 测试
~~~
curl http://localhost:8001/
~~~

## issue处理

目前代码还不具备开源的条件，我们使用这个[github的repo](https://github.com/polaristech-io/kong_mysql)用来跟踪issue。如果大家喜欢这个功能，可以给这个repo点赞。如果能到1K Star，就开一个pr把代码提交到kong社区。

## 版本

目前这个下载的是基于kong 0.14的社区版；针对kong 1.x社区版的开发在进行中。好用了之后也会放出下载。
