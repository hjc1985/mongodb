## Linux搭建mongodb详解
##### 一、下载对应版本的源码包到自己用户家目录下
1. 通过wget命令下载

```
[root@izwz9g32ih0kwhap9ij30uz ~]# pwd
/root
[root@izwz9g32ih0kwhap9ij30uz ~]# ll
total 383704
-rw-r--r-- 1 root root 104247844 Jan 16 13:55 go1.9.2.linux-amd64.tar.gz
drwxr-xr-x 7 root root      4096 Sep 13 15:53 oneinstack
-rw-r--r-- 1 root root 288637516 Sep 13 10:01 oneinstack-full.tar.gz
-rw-r--r-- 1 root root     11303 Sep 13 14:34 wget-log
[root@izwz9g32ih0kwhap9ij30uz ~]# wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel62-3.4.4.tgz


```
2.windows下下载，通过ftp上传到对应的目录下，上传过后文件列表

```
[root@izwz9g32ih0kwhap9ij30uz ~]# ll
total 481804
-rw-r--r-- 1 root root 104247844 Jan 16 13:55 go1.9.2.linux-amd64.tar.gz
-rw-r--r-- 1 root root 100452894 Apr 21  2017 mongodb-linux-x86_64-rhel62-3.4.4.tgz
drwxr-xr-x 7 root root      4096 Sep 13 15:53 oneinstack
-rw-r--r-- 1 root root 288637516 Sep 13 10:01 oneinstack-full.tar.gz
-rw-r--r-- 1 root root     11303 Sep 13 14:34 wget-log

```
##### 二、解压源码包到安装目录下并新建相关文件
1、通过tar命令解压源码包

```
[root@izwz9g32ih0kwhap9ij30uz ~]# tar zxvf mongodb-linux-x86_64-rhel62-3.4.4.tgz
[root@izwz9g32ih0kwhap9ij30uz ~]# ll
total 481808
-rw-r--r-- 1 root root 104247844 Jan 16 13:55 go1.9.2.linux-amd64.tar.gz
drwxr-xr-x 3 root root      4096 Jan 24 17:05 mongodb-linux-x86_64-rhel62-3.4.4
-rw-r--r-- 1 root root 100452894 Apr 21  2017 mongodb-linux-x86_64-rhel62-3.4.4.tgz
drwxr-xr-x 7 root root      4096 Sep 13 15:53 oneinstack
-rw-r--r-- 1 root root 288637516 Sep 13 10:01 oneinstack-full.tar.gz
-rw-r--r-- 1 root root     11303 Sep 13 14:34 wget-log
```
2、重命名解压后源码包，并移动到对应的文件目录下(此目录自定义)

```
[root@izwz9g32ih0kwhap9ij30uz ~]# mv mongodb-linux-x86_64-rhel62-3.4.4 mongodb
[root@izwz9g32ih0kwhap9ij30uz ~]# mv mongodb /usr/local/
```
此时在/usr/local/下面就有mongodb的解压后的源码包

```
[root@izwz9g32ih0kwhap9ij30uz ~]# cd /usr/local/
[root@izwz9g32ih0kwhap9ij30uz local]# ll
total 84
drwxr-xr-x   7 root root 4096 Dec 29 15:20 aegis
drwxr-xr-x.  2 root root 4096 Sep 13 14:53 bin
drwxr-xr-x.  2 root root 4096 Nov  5  2016 etc
drwxr-xr-x.  2 root root 4096 Nov  5  2016 games
drwxr-xr-x   7 root root 4096 Sep 13 14:45 imagemagick
drwxr-xr-x. 11 root root 4096 Sep 13 14:53 include
drwxr-xr-x.  4 root root 4096 Sep 13 14:53 lib
drwxr-xr-x.  2 root root 4096 Nov  5  2016 lib64
drwxr-xr-x.  2 root root 4096 Nov  5  2016 libexec
drwxr-xr-x   3 root root 4096 Sep 13 14:31 man
drwxr-xr-x   5 root root 4096 Sep 13 14:49 memcached
drwxr-xr-x   3 root root 4096 Jan 24 17:05 mongodb
drwxr-xr-x  13 root root 4096 Sep 13 14:29 mysql
drwxr-xr-x  11 root root 4096 Sep 13 14:48 nginx
drwxr-xr-x   6 root root 4096 Sep 13 14:29 openssl
drwxr-xr-x   9 root root 4096 Sep 13 14:40 php
drwxr-xr-x   6 root root 4096 Sep 13 14:48 pureftpd
drwxr-xr-x   5 root root 4096 Sep 13 14:49 redis
drwxr-xr-x.  2 root root 4096 Nov  5  2016 sbin
drwxr-xr-x.  9 root root 4096 Sep 13 14:31 share
drwxr-xr-x.  2 root root 4096 Nov  5  2016 src

```
3、在/usr/local/mongodb新建文件夹db(用来存放mongodb数据)与logs(用来存放mongodb日志文件,次文件一定要是文件而不是文件夹),以上文件夹路劲以及文件名均可自定义


```
[root@izwz9g32ih0kwhap9ij30uz local]# cd mongodb/
[root@izwz9g32ih0kwhap9ij30uz mongodb]# mkdir db
[root@izwz9g32ih0kwhap9ij30uz mongodb]# touch logs
[root@izwz9g32ih0kwhap9ij30uz mongodb]# ll
total 128
drwxr-xr-x 2 root root  4096 Jan 24 17:05 bin
drwxr-xr-x 2 root root  4096 Jan 24 17:21 db
-rw-r--r-- 1 root root 34520 Apr 21  2017 GNU-AGPL-3.0
drwxr-xr-x 2 root root  4096 Jan 24 17:21 logs
-rw-r--r-- 1 root root 16726 Apr 21  2017 MPL-2
-rw-r--r-- 1 root root  1359 Apr 21  2017 README
-rw-r--r-- 1 root root 55625 Apr 21  2017 THIRD-PARTY-NOTICES

```
4、在/usr/local/mongodb/bin目录下新建mongodb.conf配置文件,配置内容如下

```
port=27017  //momgodb默认占用的端口
dbpath=/usr/local/mongodb/db   //数据库文件位置
logappend=true   //# 以追加方式写入日志
fork=true    //是否以守护进程方式运行
logpath=/usr/local/mongodb/logs   //日志文件位置,这些都是可以自定义修改的
nohttpinterface=true  //禁用http界面，默认为localhost：28017
#auth = true   //是否开启权限验证
```
特别提醒：以上文件都以root权限操控，不然在启动mongod服务，会读取不了对应的配置文件

##### 三、启动mongodb服务并配置启动项

1、启动mongodb服务

```
[root@izwz9g32ih0kwhap9ij30uz bin]# ./mongod --config=/usr/local/mongodb/mongodb.conf
about to fork child process, waiting until server is ready for connections.
forked process: 28403
child process started successfully, parent exiting
[root@izwz9g32ih0kwhap9ij30uz mongodb]# ps -ef | grep mongodb
root     28403     1  1 15:51 ?        00:00:01 ./mongod --config=/usr/local/mongodb/mongodb.conf

```
2、设置为开机自启，并配置service服务.切换到/etc/init.d/目录下，新建文件mongodb，并编辑脚本类容

```
[root@izwz9g32ih0kwhap9ij30uz ~]# cd /etc/init.d/
[root@izwz9g32ih0kwhap9ij30uz init.d]# vim mongodb
```
mongodb文件内容如下：
```
#!/bin/sh
#
#chkconfig:2345 80 90
#description: mongodb

if test -f /sys/kernel/mm/transparent_hugepage/enabled; then
   echo never > /sys/kernel/mm/transparent_hugepage/enabled
fi
if test -f /sys/kernel/mm/transparent_hugepage/defrag; then
   echo never > /sys/kernel/mm/transparent_hugepage/defrag
fi

start() {
        /usr/local/mongodb/bin/mongod -f /usr/local/mongodb/bin/mongodb.conf
}
stop() {
        /usr/local/mongodb/bin/mongod -f /usr/local/mongodb/bin/mongodb.conf --shutdown
}

case "$1" in
  start)
     start
     ;;
  stop)
     stop
     ;;
  restart)
     stop
     start
     ;;
   *)
  echo $"Usage: $0 {start|stop|restart}"
  exit 1
esac

```
3、使脚本生效(Linux下chkconfig命令详解,友情链接：https://www.cnblogs.com/panjun-Donet/archive/2010/08/10/1796873.html)

```
[root@izwz9g32ih0kwhap9ij30uz init.d]# chkconfig --add mongodb
[root@izwz9g32ih0kwhap9ij30uz init.d]# chmod +x  mongodb
[root@izwz9g32ih0kwhap9ij30uz init.d]# chkconfig mongodb on

```
4、利用service指令启动mongodb

```
[root@izwz9g32ih0kwhap9ij30uz init.d]# ps -ef | grep mongodb
root     28403     1  0 15:51 ?        00:00:17 ./mongod --config=/usr/local/mongodb/mongodb.conf
root     28836 28536  0 16:47 pts/1    00:00:00 grep --color mongodb
[root@izwz9g32ih0kwhap9ij30uz init.d]# service mongodb stop
killing process with pid: 28403
[root@izwz9g32ih0kwhap9ij30uz init.d]# service mongodb start
about to fork child process, waiting until server is ready for connections.
forked process: 28878
child process started successfully, parent exiting
[root@izwz9g32ih0kwhap9ij30uz init.d]# service mongodb
Usage: /etc/init.d/mongodb {start|stop|restart}
[root@izwz9g32ih0kwhap9ij30uz init.d]# 
```
##### 四、给mongodb配置权限访问
1、关闭配置文件/usr/local/mongodb/bin/mongodb.conf里面的auth认证

```
#auth = true   //是否开启权限验证
```
2、使用命令行进入mongodb目录，输入mongo命令，进入mongodb客户端

```
[root@izwz9g32ih0kwhap9ij30uz bin]# ./mongo
MongoDB shell version v3.4.4
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 3.4.4
Server has startup warnings: 
2018-01-25T16:47:37.305+0800 I STORAGE  [initandlisten] 
2018-01-25T16:47:37.305+0800 I STORAGE  [initandlisten] ** WARNING: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine
2018-01-25T16:47:37.305+0800 I STORAGE  [initandlisten] **          See http://dochub.mongodb.org/core/prodnotes-filesystem
2018-01-25T16:47:37.600+0800 I CONTROL  [initandlisten] 
2018-01-25T16:47:37.600+0800 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2018-01-25T16:47:37.600+0800 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2018-01-25T16:47:37.600+0800 I CONTROL  [initandlisten] ** WARNING: You are running this process as the root user, which is not recommended.
2018-01-25T16:47:37.600+0800 I CONTROL  [initandlisten] 
> 
```
***由于没有开启权限验证，所以有warming警告！

3、查看当前数据库情况，并新建一个管理员用户

```
> show dbs
admin  0.000GB
local  0.000GB
> use admin
switched to db admin
> db.createUser({user: "admin", pwd: "123456", roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]})
Successfully added user: {
	"user" : "admin",
	"roles" : [
		{
			"role" : "userAdminAnyDatabase",
			"db" : "admin"
		}
	]
}
> 
> show collections
system.users
system.version
> 

```
此时，存在两个集合，一个是用户集合，一个是系统自带的版本集合，分别查看集合里面的内容如下：

```
> db.system.users.find()
{ "_id" : "admin.admin", "user" : "admin", "db" : "admin", "credentials" : { "SCRAM-SHA-1" : { "iterationCount" : 10000, "salt" : "Ax14P7XjjOm8aLjKpjA0BQ==", "storedKey" : "wojyo+fR//1UHfyUZ+8Ry1fbYrg=", "serverKey" : "O6IQV9wtxRbJtuHM/1MBQOcWto0=" } }, "roles" : [ { "role" : "userAdminAnyDatabase", "db" : "admin" } ] }
> db.system.version.find()
{ "_id" : "featureCompatibilityVersion", "version" : "3.4" }
{ "_id" : "authSchema", "currentVersion" : 5 }
> 

```

4、开启权限认证并检测是否生效(取消配置文件里面的注释#auth=true),重启mongodb服务

```
[root@izwz9g32ih0kwhap9ij30uz init.d]# vim /usr/local/mongodb/bin/mongodb.conf 
[root@izwz9g32ih0kwhap9ij30uz init.d]# service mongodb restart

```
进入客户端操作数据库结果如下：

```
[root@izwz9g32ih0kwhap9ij30uz bin]# ./mongo
MongoDB shell version v3.4.4
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 3.4.4
> show dbs
2018-01-26T10:32:32.295+0800 E QUERY    [thread1] Error: listDatabases failed:{
	"ok" : 0,
	"errmsg" : "not authorized on admin to execute command { listDatabases: 1.0 }",
	"code" : 13,
	"codeName" : "Unauthorized"
} :
_getErrorWithCode@src/mongo/shell/utils.js:25:13
Mongo.prototype.getDBs@src/mongo/shell/mongo.js:62:1
shellHelper.show@src/mongo/shell/utils.js:769:19
shellHelper@src/mongo/shell/utils.js:659:15
@(shellhelp2):1:1

```
报错根据说明，提示权限验证失败，说明权限生效，现在输入验证机制，操作如下：

```
> use admin
switched to db admin
> db.auth("admin","123456")
1
> show dbs
admin  0.000GB
local  0.000GB
> 

```
db.auth("admin","123456")返回1，说明验证通过，现在可以快乐的玩耍我们的mongodb数据库啦！
##### 五、如果是php操作mongodb数据库，且mongbdb版本是3.0以上请注意：

在3.0版之后的Mongodb，shell中依旧可以使用上述方法验证，但是php认证一直失败，日志中会报错（ Failed to authenticate myuser@userdb with mechanism MONGODB-CR: AuthenticationFailed MONGODB-CR credentials missing in the user document），原来新版的mongodb加入了SCRAM-SHA-1校验方式，需要第三方工具配合进行验证。

下面给出具体解决办法：  
首先关闭认证，修改system.version文档里面的authSchema版本为3，初始安装时候应该是5，命令行如下： 

```
> use admin 
switched to db admin 
>  var schema = db.system.version.findOne({"_id" : "authSchema"}) 
> schema.currentVersion = 3 
3 
> db.system.version.save(schema) 
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 }) 
```

不过如果你现在开启认证，仍然会提示AuthenticationFailed MONGODB-CR credentials missing in the user document 
原因是原来创建的用户已经使用了SCRAM-SHA-1认证方式 

```
> use admin 
> db.auth('admin','123456')
> db.system.users.find()
{ "_id" : "admin.admin", "user" : "admin", "db" : "admin", "credentials" : { "SCRAM-SHA-1" : { "iterationCount" : 10000, "salt" : "Ax14P7XjjOm8aLjKpjA0BQ==", "storedKey" : "wojyo+fR//1UHfyUZ+8Ry1fbYrg=", "serverKey" : "O6IQV9wtxRbJtuHM/1MBQOcWto0=" } }, "roles" : [ { "role" : "userAdminAnyDatabase", "db" : "admin" } ] }
```
解决方案是将原来的用户删掉，重新分配用户，步骤依照上面即可！






















