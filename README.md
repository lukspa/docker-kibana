[![](https://images.microbadger.com/badges/image/khezen/kibana.svg)](https://hub.docker.com/r/khezen/kibana/)
# Supported tags and respective `Dockerfile` links

* `5.0.0`, `5.0`, `5`, `latest` [(5.0/Dockerfile)](https://github.com/Khezen/docker-kibana/blob/5.0/Dockerfile)

# What is Kibana?
Kibana lets you visualize your Elasticsearch data and navigate the Elastic Stack, so you can do anything from learning why you're getting paged at 2:00 a.m. to understanding the impact rain might have on your quarterly numbers.

[<img src="https://static-www.elastic.co/fr/assets/blt282ae2420e32fc38/icon-kibana-bb.svg?q=802" width="144" height="144">](https://www.elastic.co/fr/products/kibana)

# How To Use

## docker engine

```
docker run -d -p 5601:5601 khezen/kibana:latest   
```

## docker-compose

### [File Descriptors and MMap](https://www.elastic.co/guide/en/elasticsearch/guide/current/_file_descriptors_and_mmap.html)

run the following command on your host:
```
sysctl -w vm.max_map_count=262144
```
You can set it permanently by modifying `vm.max_map_count` setting in your `/etc/sysctl.conf`.

### docker-compose.yml
```
version: '2'
services:
    elasticsearch:
        image: khezen/elasticsearch
        environment:
            ELASTIC_PWD: changeme
            KIBANA_PWD: brucewayne
        ports:
             - "9200:9200"
             - "9300:9300"
        network_mode: bridge
        restart: always

    kibana:
        links:
            - elasticsearch
        image: khezen/kibana:5
        environment:
            KIBANA_PWD: brucewayne
        ports:
             - "5601:5601"
        network_mode: bridge
        restart: always

```
# Environment Variables

##### KIBANA_PWD | `changeme`
password for elasticsearch built-in user *kibana*.

##### ELASTICSEARCH_HOST | `elasticseach`
Elasticsearch hostname.

##### ELASTICSEARCH_PORT | `9200`
Elasticsearch port.

# User Feedback
## Issues
If you have any problems with or questions about this image, please ask for help through a [GitHub issue](https://github.com/Khezen/docker-kibana/issues).