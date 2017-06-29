docker-dashboard-arm
====================

[![Build Status](https://travis-ci.org/EasyPi/docker-dashboard-arm.svg?branch=master)](https://travis-ci.org/EasyPi/docker-dashboard-arm)

:bar_chart: Dashboard with Docker Containers on RaspberryPi

### How It Works

- [easypi/telegraf-arm][1] - Collect data
- [easypi/influxdb-arm][2] - Store data
- [easypi/grafana-arm][3] - Show data
- [easypi/statsd-arm][4] - Aggregate data

### Quickstart

```bash
$ git clone https://github.com/EasyPi/docker-dashboard-arm.git
$ cd docker-dashboard-arm/fig/
$ tree -F -P '*.yml'
.
├── grafana/
│   └── docker-compose.yml
├── influxdb/
│   └── docker-compose.yml
├── statsd/
│   └── docker-compose.yml
└── telegraf/
    └── docker-compose.yml

$ cd influxdb/
$ docker-compose up -d

$ cd ../telegraf/
$ docker-compose run --rm telegraf -sample-config > telegraf.conf
$ vim telegraf.conf
$ docker-compose up -d

$ cd ../grafana/
$ docker-compose up -d
```

### Screenshot

![](screenshot.png)

### Administration

If you want to delete old data (>30d), please run this InfluxDB query:

```
ALTER RETENTION POLICY default ON telegraf DURATION 30d DEFAULT
```

[1]: https://hub.docker.com/r/easypi/telegraf-arm/
[2]: https://hub.docker.com/r/easypi/influxdb-arm/
[3]: https://hub.docker.com/r/easypi/grafana-arm/
[4]: https://hub.docker.com/r/easypi/statsd-arm/
