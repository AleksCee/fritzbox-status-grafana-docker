# Anmerkung
Auf der Basis von https://github.com/pkdevel/fritzbox-status-grafana-docker habe ich das Docker file mal so angepasst, dass es läuft mit dem Stand von der Anleitung. Grafana hat in der Zwischenzeit von Ubuntu/Debian auf Alpine umgestellt und in der aktuellen Ubuntu 20.04 ging das Installieren von pip nicht.
Da die Anleitung auf einer Version von 2019 basierte, habe ich es auf Basis der Version v5.4.3 angepasst und die influxdb installation repariert.
Unterschiede zu dem orginal Projekt sind also nur im Docker File.


packed this guide into a docker image:
https://blog.butenostfreesen.de/2018/10/11/Fritz-Box-Monitoring-mit-Grafana-und-Raspberry/

# config
edit 'conf/collectd.conf' and set your fritz box's hostname and credentials

# build
```
docker build . --tag fb-grafana
```

# run
```
docker run -d --name fb-grafana \
        -p 3000:3000 \
        -v $(pwd)/conf/collectd.conf:/etc/collectd/collectd.conf.d/collectd.conf \
        -v $(pwd)/conf/influxdb.conf:/etc/influxdb/influxdb.conf \
        -v $(pwd)/conf/grafana-datasource-influxdb.yaml:/etc/grafana/provisioning/datasources/grafana-datasource-influxdb.yaml \
        -v $(pwd)/conf/grafana-dashboard-fb-status.yaml:/etc/grafana/provisioning/dashboards/grafana-dashboard-fb-status.yaml \
        -v $(pwd)/conf/grafana-dashboard-fb-status.json:/etc/grafana/provisioning/dashboards/fb-status/grafana-dashboard-fb-status.json \
        fb-grafana
```
