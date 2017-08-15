# java 探针部署

1 将探针压缩包解压，包部署到应用服务器${chuanyunPrefix}/agent目录下

2 设置jvm启动参数

>-XX:PermSize=256m -XX:MaxPermSize=256m

>-javaagent:${chuanyunPrefix}/agent/fix-bootstrap-1.0.0-SNAPSHOT.jar  

>-Dfix.applicationName=${applicationName} 

>-Dfix.log=${chuanyunPrefix}/agent/log

>-Dfix.projectEnv=${ENV}

>-Dfix.tracingLog=${chuanyunPrefix}/log/tracing/java

>-Dfix.samplingRate=${samplingRate}

3 重启应用

4 部署flume收集${chuanyuanPrefix}/log/tracing/java目录下的日志，发送到kafka中（发送到topic : cytracing）

5 如有需要，添加日志删除crontab，日志格式tracing-xxx.log.yyyy-mm-dd

6 参数说明

- ${chuanyunPrefix} 是穿云平台部署目录. exp. /var/chuanyun
-  ${applicationName} 是当前应用名， exp.
-  ${ENV} 是应用运行环境   release/sit/test
-  ${samplingRate} 是采样率， 1 是全采样，  2 是1/2采样，以此类推。
