---
layout: post
title: Setting up the elbk stack
image: /assets/img/elbk-stack-setup/cover.png
readtime: 8 minutes
---

### Update

It's worth noting, this post refers to ELBK stach version 5, the latest can be found here: [https://www.elastic.co/](https://www.elastic.co/). Also there are PAAS offerings, which means you can have a cloud provider provision a lot of the infrastructure on your behalf, without maintainance. 

## What is the ELBK stack?

Within my work life, we use the ELBK stack as an analytics platform, for getting insights into the health of the website as a whole, and also discovering patterns of behaviour about our customers, without identifying them individually.

The ELBK stack is made of many different components, but the main being:
- ElasticSearch - A document database
- Kibana - A data visualisation tool
- Beats - A data capture tool (e.g. filebeat can capture from files)
- Logstash - A data parser, which can parse data from beats and forward to ElasticSearch

### A typical setup

<amp-img src="/assets/img/elbk-stack-setup/typical-setup.png"
  width="747"
  height="145"
  layout="responsive">
</amp-img>

A typical setup would be to rotate the nginx logs on your web servers, allowing filebeat to send the data to logstash in order to be parsed and passed to elasticsearch.

Lets have a look how this might be done:

### Nginx Logging

<amp-img src="/assets/img/elbk-stack-setup/nginx.png"
  width="392"
  height="102"
  layout="responsive">
</amp-img>

You can specify the format of the logging that you need, the Nginx documentation for this is really good.
Here is a typical log format I've used in the past, it creates a log directive called logstash, which can be specified inside your location blocks

```
log_format logstash  'HTTPREQUEST [$host] [$remote_addr $time_iso8601] [$request] '
                     '[$status $body_bytes_sent] [$request_time] [$http_referer] '
                     '[$http_user_agent] [$http_cookie] '
                     '[$sent_http_content_type] [$sent_http_location] ';
```
I've surrounded each of the directives with square brackets, which should make parsing the log easier in logstash, as it will signal the start and end of each piece of data.

The above logg should output something like the below: 

```
Add example here
```


### Log Rotate

You would likely want to rotate the logs in nginx, so that they don't eventually fill up the entire server.
This can be done using logrotate, and a setup such as the below, will allow 30 days worth of logs to be kept on the server.

```
/var/log/nginx/*.log {
  daily
  create 0777 administrator administrator
  copytruncate
  rotate 30
}
```

### Logstash

<amp-img src="/assets/img/elbk-stack-setup/logstash.png"
  width="294"
  height="115"
  layout="responsive">
</amp-img>


Setting up logstash is pretty straight forward, and can be done using a script similar to the below (if you want to automate it)
Logstash depends on OpenJDK, Rub, Rake and Bundler.

```
sudo apt-get install -y openjdk-8-jdk openjdk-8-jre jruby rake bundler
[[ -f logstash-5.2.2.deb ]] && echo "logstash-5.2.2.deb exists, skipping download." || sudo wget https://artifacts.elastic.co/downloads/logstash/logstash-5.2.2.deb
sudo dpkg -i logstash-5.2.2.deb
```

Once logstash is installed, you need to update the logstash config, to provide any mutations and grokking, to get the log into a document fit for elasticsearch.

A typical logstash configuration can be seen here 

```
Example Here
```

### Elasticsearch

<amp-img src="/assets/img/elbk-stack-setup/elastic.png"
  width="477"
  height="248"
  layout="responsive">
</amp-img>

Elasticsearch is pretty easy to setup, if you want to automate it, you can use a script like the below:

```
sudo apt-get update 
sudo apt-get install -y default-jre apt-transport-https
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
sudo apt-get update && sudo apt-get install elasticsearch
```

Once it is installed, locate the elasticsearch.yml file, located at `/etc/elasticsearch/` update the file to:
- `cluster.name` use this to give an identifier to your cluster
- `network.host` to the ip address of the machine
- add cors headers to the file, but adding the following:
```
http.cors.enabled: true
http.cors.allow-origin: "*"
```

### Kibana

<amp-img src="/assets/img/elbk-stack-setup/kibana.png"
  width="306"
  height="280"
  layout="responsive">
</amp-img>

Kibana is also pretty easy to setup, if you want to automate it, you can use a script like the below:

```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
sudo apt-get install -y apt-transport-https
echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
sudo apt-get update && sudo apt-get -y install kibana
```

Once it is installed, locate the kibana.yml file, located at `/etc/kibana/`

Make sure to update
- `server.host` to the ip address of the machine
- `elasticsearch.url` to the ip address of elasticsearch
- any other changes to the file to your liking.

Browse to the kibana IP address, on port 5601 and you are up and running!! 

### Closing and Opening indexes

Using this basic setup, your elastic search instance will create a seperate index each day, so it's worth knowing how to open and close indexes, so that the quantity of data does not become too large.

Youo can do this by making a curl request to the elasticsearch instance

```
To open an index:
curl -XPOST http://elasticsearch:9200/logstash-2018.04*/_open

To open an index:
curl -XPOST http://elasticsearch:9200/logstash-2018.04*/_close

where logstash-2018.04* is the index (wildcard supported!!)
```