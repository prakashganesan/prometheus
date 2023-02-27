## Prometheus Setup 
Prometheus, a [Cloud Native Computing Foundation](https://cncf.io/) project, is a systems and service monitoring system. It collects metrics
from configured targets at given intervals, evaluates rule expressions,
displays the results, and can trigger alerts when specified conditions are observed.

# Architecture overview

![Architecture overview](https://cdn.jsdelivr.net/gh/prometheus/prometheus@c34257d069c630685da35bcef084632ffd5d6209/documentation/images/architecture.svg)

# Config file info

We going to setup Prometheus, Alert Manager and Nginx in our example

* ```docker-compose.yml``` Docker compose file configured with required container's setup to run in our local machine
* ```prometheus.yml``` configuration file will be copied to prometheus container and this configuration file will be used during the service startup.
* ```nginx.conf``` configuration file configured with ```stub_status``` to provide the metrics to ```nginx node exporter```
* ```nginx_alert_rules.yml``` configuration file has the alert rules to trigger when nginx container goes down.

**Docker Compose Install in Ubuntu**
Ref: https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository

### Prometheus up and running

* Command to start the docker compose
![Docker Compose up](./images/Docker-Compose-Up.PNG)

* Prometheus status 
![Prometheus](./images/Prometheus-up.PNG)

* Targets configured in Prometheus
![Prometheus-targets](./images/Prometheus-targets.PNG)

* Nginx alert configuration info
![Nginx-alert](./images/nginx-alert.PNG)

* Nginx alert rules info
![Nginx-alert-rules](./images/nginx-alert-rules.PNG)

* Available nginx plugins to pull the metrics from the nginx
![Nginx-metrics](./images/nginx-metrics.PNG)

Let's stop the nginx container and will check the alert status

![Nginx-container-stop](./images/nginx-container-shutdown.PNG)

Once container goes down alerts become pending state and will wait for the container state for 1m before triggering the alert

![Nginx-alert-pending](./images/nginx-container-alert-waiting-for-the-nginx-container-status.PNG)

Once the alert reaches 1m and if container is not become active then alert will get started to trigger

![Nginx-alert](./images/nginx-container-alert-after-waiting-1m-alert-triggered.PNG)

Let's start the nginx container will check the alert status 

![Nginx-container-start](./images/nginx-container-start.PNG)

Once container become active alert will get recovered

![Nginx-alert-recovery](./images/nginx-alert-recovered.PNG)


