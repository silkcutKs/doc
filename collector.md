# file log collector


## how

use logstash (2.4.0), java 1.7 support

https://www.elastic.co/downloads/past-releases/logstash-2-4-0


logstash config


```config
# get trace log
# input

input {
     file {
         path => [
             "${chuanyun_prefix}/log/tracing/java/*.log",
             "${chuanyun_prefix}/log/tracing/php/*"
         ]
     }
}

output {
     kafka {
         codec => plain {
            format => "%{message}"
         }
         topic_id => test1
         bootstrap_servers => "localhost:9092"
         compression_type => snappy
         workers => 2
     }
}
```
