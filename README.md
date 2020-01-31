# zabbix-mtr-ping

cd /opt/

git clone https://github.com/GamePorxyLSP/zabbix-mtr-ping.git

cp -fv /opt/zabbix-mtr-ping/UserParams.conf /etc/zabbix/zabbix_agentd.d/zabbix_mtr_ping.conf

chmod +x /opt/zabbix-mtr-ping/zabbix_mtr.sh

chown root /usr/sbin/mtr

chmod u+s /usr/sbin/mtr

sed -i '/Server=/s/127.0.0.1/117.28.254.80/' /etc/zabbix/zabbix_agentd.conf

sed -i '/ServerActive=/s/127.0.0.1/117.28.254.80/' /etc/zabbix/zabbix_agentd.conf

sed -i "s/# Timeout=3/Timeout=30/" /etc/zabbix/zabbix_agentd.conf

sed -i "# StartAgents=3/StartAgents=10/" /etc/zabbix/zabbix_agentd.conf

service zabbix-agent restart

sudo -H -u zabbix /opt/zabbix-mtr-ping/zabbix_mtr.sh -n -c 3 8.8.8.8


Open Zabbix Menu:
Configuration -> Templates -> Import

Choose Template_Zabbix_MTR_Example.xml

## Modify Items, Triggers and Graphs for your latency and destination hosts requirements
