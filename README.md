# jdbcDB2Status
Check Health DB2 via JDBC

Files:
- **jdbDB2Status.java**: File with code.
- **hosts_db2.txt**: DB2's to check

# My example and case of use:

Include jar into crontab to check every 5 minutes the health, save in Elastic, and show in Kibana.

> Create a folder: "DB2Status" in /opt/ for example and include into crontab

```sh
*/5 * * * * cd /opt/DB2Status/ && java -cp "/opt/DB2Status:/opt/DB2Status/jdbcDB2Status.jar:/opt/DB2Status/db2jcc.jar:/opt/DB2Status/db2jcc.jar:db2jcc_license_cu.jar" jdbcDB2Status
```

# Create jar file

```sh
jar cfe jdbDB2Status.jar jdbDB2Status jdbDB2Status.class
```
Example json in Kibana:

```json
{
  "_index": "monitor-2018.06.13",
  "_type": "fluentd",
  "_id": "XXXXXXX",
  "_version": 1,
  "_score": null,
  "_source": {
    "primary_class": "BBDD",
    "secondary_class": "DB2",
    "host": "host:port",
    "message": "Connection to DB2 successful!",
    "status": "OK",
    "@timestamp": "2018-06-13T09:50:01.806242367+02:00",
    "tag": "monitor"
  }
}
```