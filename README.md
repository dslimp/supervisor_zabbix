# Supervisor applications checks

## Overview

Cheeck uptime, status applications supervisord



## Author

Dmitriy (https://github.com/dslimp)

## Macros used

|Name|Description|Default|Type|
|----|-----------|-------|----|
|`{$SUPERVISOR_SOCKET}`| Path to supervisord docket | /var/run/supervisor.sock | Text macro |

## Template links
- [zabbix_template_supervisord.xml](zabbix_template_supervisord.xml)

## Script Links
- [script/supervisord.py](script/supervisord.py)

## Instructions
- Download the [script/supervisord.py](script/supervisord.py) script from this repository and place it in zabbix script directory
- Run `chmod +x supervisord.py` to make the script executable
- Test executing the script from the CLI of your Zabbix server by running the python script inputing the command and socket  like `./supervisord.py discovery /var/run/supervisor.sock`
- Make sure the output is either applications and have not error
- Download and install [supervisord.conf](supervisord.conf) to zabbix_agent.d directory
- Once the script works OK, download the[zabbix_template_supervisord.xml](zabbix_template_supervisord.xml) Zabbix template from this repository and import it into your Zabbix server
- Apply the imported template to the host
- Check the latest data to make sure you are getting the proper value from the script

## Discovery rules

supervisord_discovery 

## Items collected

|Name|Description|Type|Key and additional info|
|----|-----------|----|----|
| Update supervisor raw data | Collected data | `External check` | supervisor_raw[["{HOSTNAME}", "{$GITLAB_TOKEN}"] |


## Triggers

|Name|Description|Expression|Priority|
|----|-----------|----------|--------|
| 	No data supervisor 10 min | A non-critical software update is available | `{gitlab.verticalcomputers.com:gitlab_update_check.sh["{HOSTNAME}", "{$GITLAB_TOKEN}"].str(up-to-date)}<>1` | Warning |
| Supervisor error get status | A critical software update is available | `{gitlab.verticalcomputers.com:gitlab_update_check.sh["{HOSTNAME}", "{$GITLAB_TOKEN}"].str(update asap)}=1` | High |
Service {#SUPERVISOR_PROCESS_NAME} fail
Service {#SUPERVISOR_PROCESS_NAME} inifinity restart
Service {#SUPERVISOR_PROCESS_NAME} uptime < 60 sec		
