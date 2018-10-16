---
lang: en
title: "Prometheus"
subtitle: "Combining application and infrastructure monitoring"
---

## Me

![](assets/img/hannes.jpg "Hannes"){height=300px style="border:none"}

Sysadmin @ Tradebyte

![](assets/img/tradebyte.png "Tradebyte"){width=150px  style="border:none;vertical-align=middle"}

## Agenda

1. What is it?
3. How does it work?
4. How does it work **at Tradebyte**?

## Prometheus

* by SoundCloud
* similar to Google's borgmon
* now independent open source project
* part of CNCF

::: notes
Nearly 20.000 stars on github
:::

## Prometheus

* Simple data model
* Very powerful, flexible

## Architecture

![](assets/img/architecture.png "Architecture"){style="box-shadow:none;border:none;vertical-align=middle"}

::: notes
* pull based
* http
* ingest everything
:::

## Metrics

```
http_requets_total 514.0
```

## Metrics

```
http_requets_total{response="200"} 514.0
```

> * always a float
> * export via HTTP

::: notes
counters or gauges
:::

## Exporters

* Listen of HTTP requests
* Return metrics

## Node exporter

```
[...]
node_load1 0.68
node_load5 1.14
node_load15 1.42
node_memory_MemFree_bytes 5.730304e+08
node_memory_MemTotal_bytes 3.381096448e+10
node_network_receive_bytes_total{device="eth0"} 8.0238013e+12
node_network_receive_errs_total{device="eth0"} 0
[...]
```

## MySQL

```
[...]
mysql_up 1
mysql_slave_status_seconds_behind_master 0
mysql_slave_status_slave_sql_running 1
mysql_slave_status_slave_io_running 1
[...]
```

## Exporters

* PostgreSQL
* ElasticSearch
* RabbitMQ
* Ceph
* Apache
* Nginx
* Docker
* GitHub
* Kubernetes
* ...

## Write your own exporter!

## Python

```py
import prometheus_client as prom

class MyCollector(object):
    def collect():
        metric = prom.core.GaugeMetricFamily('my_metric')
        metric.add_metric(value=5)
        yield metric

if __name__ == '__main__':
	prom.REGISTRY.register(MyCollector())
	prom.start_http_server(8000)
	while True: time.sleep(1)
```

## Python

```shell
curl http://localhost:8000/metrics

my_metric 5
```

## Make your application export metrics

* Go
* Python/Django
* Node.js
* Clojure
* Java

## Python

```py
def long_running_function():
    do_compute()
```

## Python

```py
from prometheus_client import Summary
compute_time = Summary('compute_time')

@compute_time.time()
def long_running_function():
    do_compute()
```

Result:

```
compute_time_count 142.0
compute_time_sum 321.42
```

## What to do with metrics?

![](assets/img/simple_graph.png "Simple Graph"){style="border:none;vertical-align=middle"}

also, Grafana

## Alerting

![](assets/img/architecture.png "Architecture"){style="box-shadow:none;border:none;vertical-align=middle"}

## Alerting

![](assets/img/architecture_2.png "Architecture"){style="box-shadow:none;border:none;vertical-align=middle"}

## Alerting

```yaml
alert: InternalServerErrorResponses
expr: http_requets_total{response="500"} > 10
annotations:
  summary: "Too many 500 HTTP responses"
```

::: notes
expressions:

* sum/avg/count
* linear\_predict
* inter-host
:::

## Alertmanager

* alert batching
* alert routing

* Mail, OpsGenie, PagerDuty, Slack

## Target discovery

* Kubernetes / Marathon / OpenStack
* AWS / GCE / Azure

## Backing Storage

* InfluxDB
* PostgreSQL/TimescaleDB

## Prometheus at Tradebyte

before: Nagios / Check\_MK

currently migrating to Prometheus

::: notes
nagios:

* host-centric
* fixed thresholds
:::

## Prometheus at Tradebyte

* Similar architecture to Check\_MK
* Easy setup
* Steep learning curve

## Prometheus at Tradebyte

* Built ~10 custom exporters
* Very easy to do

## All-in-one Solution

* Infrastructure
* Application

→ Easy correlation

::: notes

* lots of 500s -> maybe DB servers are overloaded
* lots of 500s -> all servers are well

:::

# Thank you!
