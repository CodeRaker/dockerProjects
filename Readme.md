# Hello!

### docker-website-template
This project uses docker compose to create 3 containers; apache-php, mysql and phpmyadmin. It's meant to spawn a development environment, but can probably be modded, to create something more production ready.

1. Clone the directory
2. Start with `docker-compose up --build`

### docker-elk
This project uses docker compose to create 3 containers; elasticsearch, logstash and kibana. This is a development setup.

1. Clone the directory
2. Create the es user `groupadd elasticsearch && useradd -u 1000 -g elasticsearch elasticsearch`
3. Create the data directory `mkdir /esdata && chown elasticsearch:elasticsearch /esdata` (you can omit this, if you want to run non-persistent, but you must comment out the volume lines in the docker-compose.yml file, under the elasticsearch container).  
4. Start with `docker-compose up -d`

### docker-opendistro-elk
This project uses docker compose to create 4 containers; two elasticsearch nodes, one logstash and one kibana. This is a development setup.

1. Clone the directory
2. Start with `docker-compose up -d`
