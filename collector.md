# file log collector


## how

we use logstash as server and  betas as agent.

## beats

download:https://www.elastic.co/downloads/beats/filebeat

filename:filebeat.yml

config:
```config
filebeat.prospectors:
 - input_type: log

   # Paths that should be crawled and fetched. Glob based paths.
   paths:
     - ${chuanyun_prefix}/log/tracing/java/*.log
     - ${chuanyun_prefix}/log/tracing/php/*
   tail_files: true
 #----------------------------- Logstash output --------------------------------
 output.logstash:
   # The Logstash hosts
   hosts: ["localhost:5044"]

```
run: ./filebeat -e -c filebeat.yml

### collector

use logstash (2.4.0), java 1.7 support

https://www.elastic.co/downloads/past-releases/logstash-2-4-0


### logstash config

```config
# get trace log
# input

input {
     beats {
         port => 5044
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

### run

bin/logstash -f chuanyun.conf
