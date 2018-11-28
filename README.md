# elk-docker

ELK stack with docker

## docker-compose.yml

You need these:
- `kibana.yml`
- `logstash.yml`
- `pipeline/logstash.conf`

```yml
version: '2.4'
services:
  elasticsearch:
    hostname: elasticsearch
    container_name: elasticsearch
    image: docker.elastic.co/elasticsearch/elasticsearch:6.5.1
    environment:
      discovery.type: single-node
    mem_limit: 1500M
    ports:
      - 9200:9200
      - 9300:9300
  logstash:
    hostname: logstash
    container_name: logstash
    image: docker.elastic.co/logstash/logstash:6.5.1
    mem_limit: 700M
    ports:
      - 5044:5044
      - 9600:9600
    volumes:
      - ./pipeline/:/usr/share/logstash/pipeline/
      - ./logstash.yml:/usr/share/logstash/config/logstash.yml
  kibana:
    hostname: kibana
    container_name: kibana
    image: docker.elastic.co/kibana/kibana:6.5.1
    mem_limit: 600M
    ports:
      - 5601:5601
    volumes:
      - ./kibana.yml:/usr/share/kibana/config/kibana.yml
```

## Run

```bash
docker-compose up -d
```

## Test

```js
const request = require('request');

request.post({ url: 'http://localhost:8080/starwars/obiwan/4', form: { message: 'hello there' }}, (err, res, body) => {
  if (err) { return console.log(err); }
  console.log(body);
});
```
