---
uid: loggingConfiguration
---

# Message logging configuration
Edge Data Store writes daily log messages to flat text files in the following locations:

• Windows: *%ProgramData%/OSIsoft/EdgeDataStore/Logs*

• Linux: */usr/share/OSIsoft/EdgeDataStore/Logs*

Each message in the log displays the message severity level, timestamp, and the message itself.

## Default logging configuration and schema
By default, logging captures Information, Warning, Error, and Critical messages in the message logs.
The default logging configuration for a component on install is the following
```json
{
  "logLevel": "Information",
  "logFileSizeLimitBytes": 34636833,
  "logFileCountLimit": 31   
}
```

The schema file specifies how to formally describe the configuration parameters for message logging. 
It is located in:

• Windows: *%ProgramFiles%/OSIsoft/EdgeDataStore/Schema*

• Linux: */opt/EdgeDataStore/Schema*

### Log levels
Changing the logLevel leads to captures of logs in severity including and above the specified log level. The log levels in their increasing order of severity are as follows: Trace, Debug, Information, Warning, Error, Critical.

Table: General guidelines for setting the log level.

| **Level**                | **Description**|      
|--------------------------|-----------|
|Trace         | Logs that contain the most detailed messages. These messages may contain sensitive application data like actual received values. Generally, these messages shouldn’t be enabled in production environment. |
| Debug | Logs that can be used to troubleshoot data flow issues by logging metrics and detailed flow related information. |
| Information | Logs that track the general flow of the application. Any non-repetitive general information (like version information relating to the software at startup, what external services are being used, data source connection string, number of measurements, egress URL, change of state “Starting”, “Stopping” or configuration) can be useful for diagnosing potential application errors.  |
| Warning | Logs that highlight an abnormal or unexpected event in the application flow, but do not otherwise cause the application execution to stop. This can be used to react on unconfigured data source state, message that communication with backup failover instance has been lost, use of insecure communication channel, or any other event that could require attention, but isn’t directly impacting the flow. |
| Error | Logs that highlight when the current flow of execution is stopped due to a failure. These should indicate a failure in the current activity, not an application-wide failure. This can be used to react on invalid configuration, unavailable external endpoint, internal flow error, etc.|
| Critical | Logs that describe an unrecoverable application or system crash, or a catastrophic failure that requires immediate attention. This can be used to react on application wide failures like beta timeout expired, unable to start self-hosted endpoint, unable to access vital resource (Data Protection key file for example). |

### Log file count limit
The logFileCountLimit controls the number of days the log files are persisted before they are deleted for creation of new log files. 

## Changing logging configuration
To change the logging configuration you can 

1. Save the new configuration information in a JSON file format.
2. Run the following script (or make an equivalent REST API call):

For example, Component_Logging.json:
```json
{
  "logLevel": "Warning",
  "logFileSizeLimitBytes": 16777216,
  "logFileCountLimit": 30   
}
```


```bash
curl -i -d "@Component_Logging.json" -H "Content-Type: application/json" -X PUT http://localhost:5590/api/v1/configuration/<ComponentId>/Logging
```

&lt;ComponentId&gt; is the ComponentId of the adapter or Storage.

On successful execution, the log level change takes effect immediately during runtime. The other configurations (log file size and file count) get updated after Edge Data Store is restarted. 

### **Note:** 
If you do not specify all the parameters while changing the configuration, the specified parameters will be updated while the unspecified parameters will revert to the default schema values. 
