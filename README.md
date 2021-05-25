# zabbix-setuping-up-scheduled-reports

### [SCHEDULED REPORTS OVERVIEW](https://www.zabbix.com/documentation/current/manual/config/reports#scheduled_reports)


Bellow guide provides information on setting up Zabbix 5.4.0 scheduled reports and the `extra steps` needed. 

1) To get started, follow INSTALLATION instruction from: [SETTING UP SCHEDULED REPORTS](https://www.zabbix.com/documentation/current/manual/appendix/install/web_service)

2) Next, follow the <s>not so well documented</s> INSTALLATION instructions for Zabbix Web Service from: [ZABBIX WEB SERVICE](https://www.zabbix.com/documentation/current/manual/concepts/web_service#installation)

    For RHEL/Centos8 Distros
    ```
    dnf install zabbix-web-service.x86_64 
    ```
    Enable and Start Zabbix Web Server
    ```
    systemctl enable zabbix-web-service
    systemctl restart zabbix-web-service
    ```
    > *feel free to push instructions for other distros*
    
    For more information about `zabbix-web-server` configuration parameters, please refer to: [ZABBIX WEB SERVICE/PARAMETERS](https://www.zabbix.com/documentation/current/manual/appendix/config/zabbix_web_service#parameters) 
    
3) Install Google Chrome
    ```
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
    ```
    For RHEL/Centos8 Distros
    ```
    sudo dnf localinstall google-chrome-stable_current_x86_64.rpm
    ```
4) To setup communication between all elements involved, follow CONFIGURATION instruction from: [SETTING UP SCHEDULED REPORTS](https://www.zabbix.com/documentation/current/manual/appendix/install/web_service#configuration)

---
**_NOTE:_**
> If you upgraded from a Zabbix installation prior to 5.4, the following configuration parameters may be missing, and they need to be added to the Zabbix server configuration file.
---

Edit `/etc/zabbix/zabbix_server.conf` and Add/Uncoment the following parameters:
```
### Option: StartReportWriters
#       Number of pre-forked report writer instances.
#
# Mandatory: no
# Range: 0-100
# Default:
# StartReportWriters=0
StartReportWriters=3

### Option: WebServiceURL
#       URL to Zabbix web service, used to perform web related tasks.
#       Example: http://localhost:10053/report
#
# Mandatory: no
# Default:
# WebServiceURL=
WebServiceURL=http://localhost:10053/report
```
5) To enable communication between Zabbix frontend and Zabbix web service, follow ZABBIX FRONTEND instructions from: [SETTING UP SCHEDULED REPORTS](https://www.zabbix.com/documentation/current/manual/appendix/install/web_service)

6) For Scheduled Reports CONFIGURATION, please follow instructions from: [SCHEDULED REPORTS/CONFIGURATION](https://www.zabbix.com/documentation/current/manual/config/reports#configuration)

7) To finalize and test the Scheduled Reports, please follow TESTING instructions from: [SCHEDULED REPORTS/TESTING](https://www.zabbix.com/documentation/current/manual/config/reports#configuration)

---
### Throubleshooting:
- Issue: `Report generation test failed: The Frontend URL has not been configured`
![image](https://user-images.githubusercontent.com/60859142/119564921-37e3ea80-bda1-11eb-99d0-478baea602d0.png)

Solution: https://www.zabbix.com/forum/zabbix-help/425283-frontend-url-error
