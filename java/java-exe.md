# java端程序 运行于 fullnode 上，收集chia farm summary返回结果，

运行方式：
下载chia-monitor-0.0.1.zip压缩文件，之后到本地解压到X目录下。之后按照如下方式运行

X\cmr.exe  回车，查看参数详细说明 

```
D:\chia-monitor>cmr.exe
Option "-appPath" is required
cmr arguments...
 -appPath VAL                : chia app location. eg: \n linux platform:
                               /usr/local/src/chia-blockchain  \n windows
                               platform: C:\Users\Administrator\AppData\Local\ch
                               ia-blockchain\app-1.2.7\resources\app.asar.unpack
                               ed\daemon
 -appToken VAL               : If -sendWxPusher was set , require -appToken
                               abc123
 -influxDBDatabase VAL       : influxDB database
 -influxDBPassword VAL       : influxDB password
 -influxDBUrl VAL            : influxDB url
 -influxDBUsername VAL       : influxDB username
 -interval N                 : monitor schedule interval (unit: SECONDS)
 -lolpAppId VAL              : lolp authorize app id, provide by admin
 -lolpSecret VAL             : lolp authorize secret code, provide by admin
 -platform [WINDOWS | LINUX] : what system app running at. eg.linux ->
                               -platform LINUX   windows -> -platform WINDOWS
 -sendWxPusher               : If the warn message send to WX pusher , add this
                               arg '-sendWxPusher'  (default: false)
 -uids VAL                   : If -sendWxPusher was set  , require -uids user1
                               (or multi users split with ','  -uids
                               user1,user2,user3 )

 example: cmr.exe -appPath VAL -appToken VAL -influxDBDatabase VAL -influxDBPassword VAL -influxDBUrl VAL -influxDBUsername VAL -interval N -lolpAppId VAL -lolpSecret VAL -lolpUrl VAL -platform [WINDOWS | LINUX] -sendWxPusher -uids VAL

```


参数 [-sendWxPusher] [-appToken] [-uids] 为可选的参数   : 带有这三个参数,代表发送wx报警 
(相关wx pusher请看https://wxpusher.dingliqc.com/docs 快速接入部分)，需要获得一个appToken 和 自己的uid 
```
 -sendWxPusher -appToken XYZ_ASDFASDFASDF  -uids user111,user222,user333
```



参数 [-interval] 调用 chia farm summary 命令的频率，单位为秒，不能小于5秒
```
-interval 300
```


参数 [-influxDBUrl] [-influxDBDatabase] [-influxDBUsername] [-influxDBPassword] 是influxdb的url, 数据库名称，用户名与密码等相关设置



参数 [-platform]  WINDOWS 或者 LINUX


参数 [-appPath]  为chia.exe 所在的具体路径 比如: C:\Users\abc\AppData\Local\chia-blockchain\app-1.2.9\resources\app.asar.unpacked\daemon



参数 [-lolpAppId] [-lolpSecret] 认证服务器使用 ，当前可以默认设置为 -lolpAppId CH001-B92NKEA9  -lolpSecret CH001-LX1LFA37UCH0LJC8 （到期日为 2022-02-14）
```
 -lolpAppId  xxx  -lolpSecret yyy 
```


cmd example:
```
d:\cmr.exe -sendWxPusher -appToken XYZ_ASDFASDFASDF -uids user1,user2,user3 -interval 5 -influxDBUrl http://123.45.6.7:8086 -influxDBDatabase chia_monitor -influxDBUsername telegraf -influxDBPassword telegraf -platform WINDOWS -appPath C:\Users\abc\AppData\Local\chia-blockchain\app-1.2.9\resources\app.asar.unpacked\daemon -lolpAppId CH001-B92NKEA9 -lolpSecret CH001-LX1LFA37UCH0LJC8
```
