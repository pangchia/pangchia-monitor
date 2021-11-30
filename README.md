# pangchia-monitor
pangchia monitor bla bla bla




### 涉及到的开源程序 
* grafana (v8.2.2)   
* influxdb (v1.8.10)
* telegraf (v1.20.3)

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



### ***启动***   
(默认os选择ubuntu，windows环境路径有所差别，其他区别不大)



+ grafana

    ##### 确认启动、停止是否正常
    systemctl stop grafana-server.service 
    systemctl start grafana-server.service

    启动后查看进程
    ```
    ps -ef |grep grafana
    grafana     2227       1  0 11月21 ?      00:17:17 /usr/sbin/grafana-server --config=/etc/grafana/grafana.ini --pidfile=/run/grafan/grafana-server.pid --packaging=deb cfg:default.paths.logs=/var/log/grafana cfg:default.paths.data=/var/lib/grafana cfg:default.paths.plugins=/var/lib/grafana/plugins cfg:default.paths.provisioning=/etc/grafana/provisioning
    root      325850  324290  0 18:13 pts/0    00:00:00 grep --color=auto grafana 
    
    ```


+ influxdb

    ##### 确认启动、停止是否正常
    systemctl stop influxdb.service
    systemctl start influxdb.service

    启动后查看进程
    ```
    root@x99-wells-2678-192:/usr/local/src# ps -ef|grep influxdb
    influxdb    1240       1  0 11月21 ?      00:12:45 /usr/bin/influxd -config /etc/influxdb/influxdb.conf
    root      325932  324290  0 18:17 pts/0    00:00:00 grep --color=auto influxdb
    
    ```


+ telegraf

    ##### 确认启动、停止是否正常
    systemctl start telegraf.service
    systemctl stop telegraf.service

    启动后查看进程

    ```
    root@x99-wells-2678-192:/usr/local/src# ps -ef|grep telegraf   
    root        1025       1  0 11月21 ?      00:17:38 /usr/bin/telegraf -config /etc/telegraf/telegraf.conf -config-directory /etc/telegraf/telegraf.d
    root      326059  324290  0 18:21 pts/0    00:00:00 grep --color=auto telegraf
    ```








## ***配置***



+ grafana

    安装后默认配置文件: /etc/grafana/grafana.ini
    默认log: /var/log/grafana/grafana.log

    grafana默认3000端口，使用 http://你机器的IP:3000/
    比如:http://192.168.3.14:3000/

    安装后默认配置，登录用户名与密码为  admin  admin
    grafana.ini中其他配置项应该不用改动




+ influxdb

    安装后默认配置文件: /etc/influxdb/influxdb.conf
    influxdb.conf中其他配置项应该不用改动


+ telegraf

    安装后默认配置文件: /etc/telegraf/telegraf.conf

    日志过滤按照节点类型粗略残暴的分了两种 ,两种节点 telegraf.conf 配置略有不同
    
    A.fullnode   
    B.harvester 
    
    老夫目前 fullnode使用windows ,harvester使用ubuntu  各位可以按照自己的情况自行调整

    使用文件夹中的telegraf.conf替换安装时默认的配置文件telegraf.conf

    A. fullnode telegraf 配置

    fullnode: windows 如果没有默认 telegraf.conf 直接复制到 telegraf.exe 相同的文件夹
    运行:  C:/soft_setup/telegraf-1.20.3/telegraf.exe --config telegraf.conf

    工程中fullnode文件夹里telegraf.conf文件以下带有路径、IP的地方需要替换为你自己fullnode机器的路径、IP

    1. 
    ```
      logfile = "C:/soft_setup/telegraf-1.20.3/telegraf.log"
    ```

    2.
    ```
      [[outputs.file]] 
        files = ["C:/telegraf/metrics.out"]

    ```
    3.
    ```
      [[outputs.influxdb]]
        urls = ["http://192.168.3.14:8086"]

    ```
    4.  chia debug.log 路径
    ```
     [[inputs.tail]]

      name_override = "chia_log_monitor"

      files = ["C:/Users/Administrator/.chia/mainnet/log/debug.log"]

    ```

    B.  harvester telegraf 配置

    harvester: 替换ubuntu原有的文件 /etc/telegraf/telegraf.conf
    systemctl start telegraf.service  启动是会找默认位置 /etc/telegraf/telegraf.conf

    工程中harvester文件夹里telegraf.conf文件以下带有路径、IP的地方需要替换为你自己harvester机器的路径、IP

    1. 
    
    ```
     logfile = "/var/log/telegraf/telegraf.log"

    ```


    2.
    ```
    [[outputs.file]]
      files = ["/tmp/metrics.out"]

    ```


    3.
    ```
    [[outputs.influxdb]]

      urls = ["http://192.168.3.14:8086"]

    ```

    4. chia debug.log 路径
    ```

      files = ["/root/.chia/mainnet/log/debug.log"]

    ```