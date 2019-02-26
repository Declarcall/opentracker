## 软件官网

https://erdgeist.org/arts/software/opentracker/


## 作者邮箱

erdgeist@erdgeist.org

## 使用方法

下面中文的，方便讲解使用 Centos 6.9 x64位安装说明

```
yum -y install unzip wget gcc zlib-devel
wget https://github.com/1265578519/OpenTracker/archive/master.zip -O /root/OpenTracker.zip
unzip OpenTracker.zip
mv OpenTracker-master /home
cd /home
cd OpenTracker-master
cd libowfat
make
cd /home/OpenTracker-master
cd opentracker
make
```

运行程序，并且监听tcp和udp端口的8080，并且自动后台工作

```
./opentracker -p 8080 -P 8080 &
```

多端口可以加多个即可

```
./opentracker -p 8080 -P 8080 -p 6961 -P 6961 -p 2710 -P 2710 &
```

输入下方命令可以查看是否在工作中

```
top -b -n 1 |grep opentracker
```

通过浏览器访问程序的统计功能

```
http://ip:8080/stats
http://ip:8080/stats?mode=everything
```

软件的自带帮助说明

```
Usage: ./opentracker [-i ip] [-p port] [-P port] [-r redirect] [-d dir] [-u user] [-A ip] [-f config] [-s livesyncport]
	-f config include and execute the config file
	-i ip     specify ip to bind to (default: *, you may specify more than one)
	-p port   specify tcp port to bind to (default: 6969, you may specify more than one)
	-P port   specify udp port to bind to (default: 6969, you may specify more than one)
	-r redirecturlspecify url where / should be redirected to (default none)
	-d dir    specify directory to try to chroot to (default: ".")
	-u user   specify user under whose priviliges opentracker should run (default: "nobody")
	-A ip     bless an ip address as admin address (e.g. to allow syncs from this address)

Example:   ./opentracker -i 127.0.0.1 -p 6969 -P 6969 -f ./opentracker.conf -i 10.1.1.23 -p 2710 -p 80
```

间隔可以在编译前进行修改，默认我改成了2小时，以便降低服务器宽带开销

```
trackerlogic.h:#define OT_CLIENT_REQUEST_INTERVAL (60*30)
trackerlogic.h:##define OT_PEER_TIMEOUT 45
```

utorrent中制作种子过程tracker写 

```
http://你的服务器ip:8080/announce

udp://你的服务器ip:8080/announce
```


