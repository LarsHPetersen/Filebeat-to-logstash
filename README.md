# Filebeat-to-logstash

## /etc/filebeat/filebeat.yml

Comment out `output.elasticsearch:` and `hosts: ["localhost:9200"]`

uncomment `output.logstash:` and ["logstashhost:5044"]

## /etc/logstash/logstash.yml


## /etc/logstash/conf.d/beats-to-logstash.conf

input {
    beats {
        port => "5044"
    }
}
# The filter part of this file is commented out to indicate that it is
# optional.
# filter {
#
# }
output {
    stdout { codec => rubydebug }
}

## Test beats-to-logstash.conf

```bash
cd /etc/logstash/conf.d/

/usr/share/logstash/bin/logstash -f beats-to-logstash.conf --config.test_and_exit

/usr/share/logstash/bin/logstash -f beats-to-logstash.conf --config.reload.automatic
```