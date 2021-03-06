# Instructions

## docker-website-template
This project uses docker compose to create 3 containers; apache-php, mysql and phpmyadmin. It's meant to spawn a development environment, but can probably be modded, to create something more production ready.

1. Clone the directory
2. Start with `docker-compose up --build`

## docker-elk
This project uses docker compose to create 3 containers; elasticsearch, logstash and kibana. This is a development setup.

1. Clone the directory
2. Create the es user `groupadd elasticsearch && useradd -u 1000 -g elasticsearch elasticsearch`
3. Create the data directory `mkdir /esdata && chown elasticsearch:elasticsearch /esdata` (you can omit this, if you want to run non-persistent, but you must comment out the volume lines in the docker-compose.yml file, under the elasticsearch container).  
4. Start with `docker-compose up -d`

## docker-opendistro-elk
This project uses docker compose to create 4 containers; two elasticsearch nodes, one logstash and one kibana. This is a development setup that builds on the Amazon Open Distro project.

#### Install containers
1. Clone the directory
2. Customize the `docker-compose.yml` file and change the "hammerheim" names, to your own.
3. Start with `docker-compose up -d`
4. To change the Open Distro login graphics, use the sample Hugin logo, or create your own and upload: `docker cp assets/open_distro_for_elasticsearch_logo_h.svg <kibana-container-id>:/usr/share/kibana/plugins/opendistro_security/public/assets/open_distro_for_elasticsearch_logo_h.svg`

#### Install Filebeat
Use a filebeat version 6.7.2 or 6.7.1 to log to logstash. On Ubuntu:
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
apt-get install apt-transport-https
echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list
apt-get update
apt install filebeat
```

Customize Filebeat and start service - or wait - and setup encryption/authentication first (next step):
```
vi /etc/filebeat/filebeat.yml
systemctl start filebeat
```

#### Setup Logstash authentication with Filebeat
Follow this link: [Logstash Authentication and Encryption with Filebeat](https://benjaminknofe.com/blog/2018/07/08/logstash-authentication-with-ssl-certificates/)
Take note of one thing. In the guide the author tells to, set mode "force-peer" in the input file for Logstash. This does not work. It must be "peer" instead.
