# elasticsearch

[Install Elasticsearch with Docker](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)

## Docker Image

[Docker @ Elastic](https://www.docker.elastic.co)

```bash
docker pull docker.elastic.co/elasticsearch/elasticsearch:6.5.1
```

## docker-compose.yml

```yml
version: '2'
services:
  elasticsearch:
    hostname: elasticsearch
    container_name: elasticsearch
    image: docker.elastic.co/elasticsearch/elasticsearch:6.5.1
    environment:
      discovery.type: single-node
    ports:
      - 9200:9200
      - 9300:9300
```
