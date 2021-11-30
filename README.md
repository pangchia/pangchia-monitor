# pangchia-monitor
pangchia monitor bla bla bla




### 涉及到的开源程序 
* grafana (v8.2.2)   
* influxdb (v1.8.10)
* telegraf (v1.20.3)
* mysql (v8.0.17)

### 可能使用到的cmd工具
* curl



### 如果未尽说明，请通知我后续补充

### 下载与安装

* grafana: [下载与安装](https://grafana.com/docs/grafana/latest/installation/)
* influxdb & telegraf (在同一页面): [下载与安装](https://portal.influxdata.com/downloads/)
* mysql: [下载与安装](https://dev.mysql.com/downloads/mysql/)


### 官方文档

* grafana: [官方文档](https://grafana.com/docs/grafana/latest/)
* influxdb: [官方文档](https://docs.influxdata.com/influxdb/v2.1/)
* telegraf: [官方文档](https://docs.influxdata.com/telegraf/v1.20/)
* mysql: [官方文档](https://dev.mysql.com/doc/refman/8.0/en/)



### 启动 (默认os选择ubuntu，windows环境路径有所差别，其他区别不大)

---
#### grafana

##### 确认启动、停止是否正常
* systemctl stop grafana-server.service 
* systemctl start grafana-server.service

启动后查看进程
```
ps -ef |grep grafana
grafana     2227       1  0 11月21 ?      00:17:17 /usr/sbin/grafana-server --config=/etc/grafana/grafana.ini --pidfile=/run/grafan/grafana-server.pid --packaging=deb cfg:default.paths.logs=/var/log/grafana cfg:default.paths.data=/var/lib/grafana cfg:default.paths.plugins=/var/lib/grafana/plugins cfg:default.paths.provisioning=/etc/grafana/provisioning
root      325850  324290  0 18:13 pts/0    00:00:00 grep --color=auto grafana 

```

---
#### influxdb

##### 确认启动、停止是否正常
* systemctl stop influxdb.service
* systemctl start influxdb.service

启动后查看进程
```
root@x99-wells-2678-192:/usr/local/src# ps -ef|grep influxdb
influxdb    1240       1  0 11月21 ?      00:12:45 /usr/bin/influxd -config /etc/influxdb/influxdb.conf
root      325932  324290  0 18:17 pts/0    00:00:00 grep --color=auto influxdb

```

---
## telegraf

##### 确认启动、停止是否正常
systemctl start telegraf.service
systemctl stop telegraf.service

启动后查看进程

```
root@x99-wells-2678-192:/usr/local/src# ps -ef|grep telegraf   
root        1025       1  0 11月21 ?      00:17:38 /usr/bin/telegraf -config /etc/telegraf/telegraf.conf -config-directory /etc/telegraf/telegraf.d
root      326059  324290  0 18:21 pts/0    00:00:00 grep --color=auto telegraf
```



---
## mysql
##### 确认启动、停止是否正常
systemctl start mysql
systemctl stop mysql

启动后查看进程
```
root@x99-wells-2678-192:/usr/local/src# ps -ef |grep mysql
root        1276       1  0 11月21 ?      00:00:00 /bin/sh /usr/local/mysql/bin/mysqld_safe --datadir=/usr/local/mysql/data --pid-file=/tmp/mysql.pid
mysql       1590    1276  0 11月21 ?      00:38:04 /usr/local/mysql/bin/mysqld --basedir=/usr/local/mysql --datadir=/usr/local/mysq/data --plugin-dir=/usr/local/mysql/lib/plugin --user=mysql --log-error=/usr/local/mysql/data/mysql-error.log --pid-file=/tmp/mysql.pid --socket=/tmp/mysql.sock --port=3306
root      326158  324290  0 18:23 pts/0    00:00:00 grep --color=auto mysql
```




## 配置

---

## grafana

默认配置文件: /etc/grafana/grafana.ini
默认log: /var/log/grafana/grafana.log

grafana默认3000端口，使用 http://你机器的IP:3000/
比如:http://192.168.3.14:3000/

可以使用默认配置，登录用户名与密码为  admin  admin



## influxdb



## telegraf



## mysql



