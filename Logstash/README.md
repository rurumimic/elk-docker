# logstash

[Running Logstash on Docker](https://www.elastic.co/guide/en/logstash/current/docker.html)

## Docker Image

[Docker @ Elastic](https://www.docker.elastic.co)

```bash
docker pull docker.elastic.co/logstash/logstash:6.5.1
```

## docker-compose.yml

[Configuring Logstash for Docker](https://www.elastic.co/guide/en/logstash/current/docker-config.html)

| Environment Variable | Logstash Setting |
|---|---|
| PIPELINE_WORKERS | pipeline.workers |
| LOG_LEVEL | log.level |
| XPACK_MONITORING_ENABLED | xpack.monitoring.enabled |

```yml
version: '2'
services:
  logstash:
    hostname: logstash
    container_name: logstash
    image: docker.elastic.co/logstash/logstash:6.5.1
    ports:
      - 5044:5044
      - 9600:9600
    volumes:
      - ./pipeline/:/usr/share/logstash/pipeline/
      - ./logstash.yml:/usr/share/logstash/config/logstash.yml
```

## logstash.yml

example: [logstash-full.yml](https://github.com/elastic/logstash-docker/blob/6.5/build/logstash/config/logstash-full.yml)

| Environment Variable | Docker Default |
|---|---|
| http.host | 0.0.0.0 |
| xpack.monitoring.elasticsearch.url | http://elasticsearch:9200 |

```yml
http.host: "0.0.0.0"
xpack.monitoring.elasticsearch.url: http://elasticsearch:9200
xpack.monitoring.elasticsearch.username: logstash
xpack.monitoring.elasticsearch.password: changeme
```

## logstash.conf

example: [logstash.conf](https://github.com/elastic/logstash-docker/blob/6.5/examples/logstash.conf)

save in `./pipeline/logstash.conf`

```yml
input {
  beats {
    port => 5044
  }
}

# The filter part of this file is commented out to indicate that it is
# optional.
filter {
  json {
    source => "message"
  }
}

output {
  stdout { codec => rubydebug }
  elasticsearch {
    hosts => "elasticsearch:9200"
    manage_template => false
    index => "filebeat-%{+YYYY.MM.dd}"
    document_type => "doc"
  }
}
```
