# MySql5.7.26安装

## 1、my.ini文件的创建

新建my.ini文件直接放到与bin同级目录，添加内容如下：

> [mysqld]
> \# 设置3306端口
> port=3306
> \# 设置mysql的安装目录
> basedir=G:\\studyTools\MySQL\mysql-5.7.26-winx64
> \# 设置mysql数据库的数据的存放目录
> datadir=G:\\studyTools\MySQL\mysql-5.7.26-winx64\Data
> \# 允许最大连接数
> max_connections=200
> \# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
> max_connect_errors=10
> \# 服务端使用的字符集默认为UTF8
> character-set-server=utf8
> \# 创建新表时将使用的默认存储引擎
> default-storage-engine=INNODB
> \# 默认使用“mysql_native_password”插件认证
> default_authentication_plugin=mysql_native_password
> [mysql]
> \# 设置mysql客户端默认字符集
> default-character-set=utf8
> [client]
> \# 设置mysql客户端连接服务端时默认使用的端口
> port=3306
> default-character-set=utf8

注意：basedir=G:\studyTools\MySQL\mysql-5.7.26-winx64中G:后面要加两根\，否则在安装过程中会出错。

![image-20200923163502780](C:\Users\LC\AppData\Roaming\Typora\typora-user-images\image-20200923163502780.png)

## 2、环境变量的添加

新建环境变量 

变量名：MYSQL_HOME

变量值：G:\studyTools\MySQL\mysql-5.7.26-winx64  （MySql文件解压放置的目录）



配置Path:

这里是win10系统，在path内添加%MYSQL_HOME%\bin

## 3、安装

以管理员方式运行打开cmd命令窗口

切换到对应的G:\studyTools\MySQL\mysql-5.7.26-winx64\bin目录下

依次输入以下两个命令即可

G:

cd G:\studyTools\MySQL\mysql-5.7.26-winx64\bin

然后执行命令

mysqld  --initialize (此时会生成data目录)

接着执行mysqld -install

mysql启动命令：net start mysql

mysql关闭命令：net stop mysql



重置密码：

mysql -u root -p

敲击回车，显示输入密码password，无需输入密码，再次敲击回车，进入mysql，命令行显示【mysql>】

\# 将数据库切换至mysql库

mysql> USE mysql
回车

\# 修改密码
mysql> UPDATE user SET password=PASSWORD(‘newpasswd’)WHERE user=’root’
回车