# pfsense-logstash-grafana

![ScreenShot](https://github.com/kiokoman/pfsense-logstash-grafana/blob/master/images/Immagine.jpg)

tested under Ubuntu, pfSense 2.4.5-p1 and 2.5.0 (RFC 3164)

suricata in legacy mode, for inline i think you only need to change "action" under grafana from "wdrop" (would drop) to "drop" < need to be tested
# howto install influxDB
https://docs.influxdata.com/influxdb/v1.8/introduction/install/

# howto install logstash
https://www.elastic.co/guide/en/logstash/current/installing-logstash.html

install influxdb plugin

/usr/share/logstash/bin/logstash-plugin install logstash-output-influxdb

# howto install Grafana

sudo apt-get install -y apt-transport-https

sudo apt-get install -y software-properties-common wget

wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -

echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

sudo apt-get update

sudo apt-get install grafana

Start the server with systemd

To start the service and verify that the service has started:

sudo systemctl daemon-reload

sudo systemctl start grafana-server

sudo systemctl status grafana-server

Configure the Grafana server to start at boot:

sudo systemctl enable grafana-server.service

to install worldmap plugin:

/usr/share/grafana/bin/grafana-cli plugins install grafana-worldmap-panel

# Configuration

edit 30-outputs.conf and change db, user, password and retention policies for influxdb.

edit 11-pfsense.conf YOU NEED TO UNCOMMENT AND CONFIGURE #database => with the location of your GeoLite2-City.mmdb !!!

For the Raspberry i suggest to set a smaller retention policy otherwise the file will become huge to the point where Influx will stop working.(Out of Memory)

https://docs.influxdata.com/influxdb/v1.8/query_language/manage-database/#modify-retention-policies-with-alter-retention-policy
