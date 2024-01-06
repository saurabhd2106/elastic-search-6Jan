**Setup Docker on ubuntu machine**

1. Update apt repository 
```
 sudo apt update -y
```
2. Install docker and docker compose 
```
sudo apt install docker docker.io docker-compose -y
```
3. Run docker without sudo
``` 
sudo usermod -aG docker $USER
newgrp docker
```


**Setup Elasticsearch using Docker**


1. Create a new docker network.

```
docker network create elastic
```

2. Pull the Elasticsearch Docker image.

```
docker pull docker.elastic.co/elasticsearch/elasticsearch:8.11.3
```

3. Start an Elasticsearch container.

```
docker run -d --name es01 --net elastic -p 9200:9200 -it -m 1GB docker.elastic.co/elasticsearch/elasticsearch:8.11.3
```

4. Verify your container is running 

```
docker ps -a
```
5. Check the logs using docker logs command

``` 
docker logs <docker_id>
```

> If your docker fails to run and throws an error related to Java virtual memory like Max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144].  Run the following command :

```
sudo sysctl -w vm.max_map_count=262144
```

6. Copy the generated elastic password and enrollment token. These credentials are only shown when you start Elasticsearch for the first time. You can regenerate the credentials using the following commands.

```
docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana

```

We recommend storing the elastic password as an environment variable in your shell. Example:

```
export ELASTIC_PASSWORD="your_password"
```

7. Copy the http_ca.crt SSL certificate from the container to your local machine.

```
docker cp es01:/usr/share/elasticsearch/config/certs/http_ca.crt .
```

**Setup Kibana using docker**

1. Pull the Kibana Docker image.

```
docker pull docker.elastic.co/kibana/kibana:8.11.3
```

2. Start a kibana container 

```
docker run -d --name kib01 --net elastic -p 5601:5601 docker.elastic.co/kibana/kibana:8.11.3
```

3. Check the docker logs. It will print a passcode to activate kibana.

```
docker logs <docker_id>
```

4. In your browser, navigate to http://<ip_addres>:5601 and enter the enrollment token that was generated when you started Elasticsearch.

5. Log in to Kibana as the elastic user with the password that was generated when you started Elasticsearch.
