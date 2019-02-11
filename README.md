systemd Service Monitoring template for Zabbix
===========================================


FEATURES
--------
* Discovery of systemd Services (whitelisted only)
* Provides alerting when a service stops or restarts

REQUIREMENTS
------------
* RHEL/CentOS/Oracle EL
* Ubuntu 16.04
* Zabbix 3.4

INSTALLATION
------------
* Server
  * Import template __Template_App_systemd_Services.xml__ file
  * Link template to host
* Agent
  * Place the following files inside /etc/zabbix/:
  * service_discovery_whitelist
  * service_restart_check.sh
  * Copy __userparameter_systemd_services.conf__ to __/etc/zabbix/zabbix\_agentd.d/userparameter\_systemd\_services.conf__
  * Restart zabbix_agent

NOTES
------------

Use the service_discovery_whitelist to add patterns for services that you want to monitor.

Testing
-------
To test that everything works use `zabbix_agentd -t` to query the statistics :

```bash
# Discover systemd services
zabbix_agentd -t "systemd.service.discovery"
zabbix_agentd -t "systemd.service.status[sshd]"
zabbix_agentd -t "systemd.service.restart[sshd]"
zabbix_agentd -t "systemd.uptime"
```
