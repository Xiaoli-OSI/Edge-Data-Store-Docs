---
uid: ModbusTCPDataSourceConfiguration
---

# Modbus TCP data source configuration

To use the Modbus TCP EDS adapter Adapter of Edge Data Store, you must configure it for the Modbus TCP data source from which it will be polling data.

## Configure Modbus TCP data source

> **Note:** You cannot modify Modbus TCP data source configurations manually. You must use the REST endpoints to add or edit the configuration.

Complete the following to configure the Modbus TCP data source:

1. Using any text editor, create a file that contains a Modbus TCP data source in JSON form. 
You can create or copy this file to any directory on a device with Edge Data Store installed.
    - For content structure, see [Modbus TCP data source example](#modbus-tcp-data-source-example). 
    - For a table of all available parameters, see [Parameters for Modbus TCP data source](#parameters-for-modbus-tcp-data-source). 
2. Save the file as _DataSource.config.json_.
3. Use any [tool](xref:managementTools) capable of making HTTP requests to execute a POST command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/<EDS adapterId>/DataSource/`. If a Modbus TCP EDS adapter is added during installation, it will have an EDS adapterId of Modbus1, which is used in the following example.

> **Note:** During installation, it is possible to add a single Modbus TCP EDS adapter which is named Modbus1. The following example uses this component name.

Example using cURL (run this command from the same directory where the file is located):

  ```bash
  curl -v -d "@DataSource.config.json" -H "Content-Type: application/json" -X POST "http://localhost:5590/api/v1/configuration/Modbus1/DataSource"
  ```

## Parameters for Modbus TCP data source

The following parameters are available for configuring a Modbus TCP data source.

| Parameter                |Required       | Type      | Description  |
|--------------------------|-----------|-----------|---------------------------------------------------|
| **IpAddress**             | Required  | string    | The IP address of the device from which the data is to be collected using the Modbus TCP protocol. Host name is not supported. |
| **Port**                  | Optional  | number | The TCP port of the target device that listens for and responds to Modbus TCP requests. The value ranges from 0 to 65535. If not configured, the default TCP port is 502 (which is the default port for Modbus TCP protocol). |
| **StreamIdPrefix**        | Optional          | number | Parameter applied to all data items collected from the data source. If not configured, the default value is the ID of the Modbus TCP EDS adapter. The custom StreamIdPrefix has the highest priority.|
| **ApplyPrefixToStreamId** | Optional          | boolean | Parameter applied to all data items collected from the data source that have custom stream ID configured. If configured, the adapter will apply the StreamIdPrefix property to all the streams with custom ID configured. The property does not affect any streams with default ID configured|
| **ConnectTimeout**        | Optional          | number  | Parameter to specify the time (in milliseconds) to wait when Modbus TCP EDS adapter is trying to connect to the data source. The value ranges from 1000 ms to 30000 ms. The default value is 5000 ms.|
| **ReconnectInterval**     | Optional          | number  | Parameter to specify the time (in milliseconds) to wait before retrying to connect to the data source when the data source is offline. The value ranges from 100 ms to 30000 ms. The default value is 1000 ms. |
|**RequestTimeout**         | Optional          | number  |Parameter to specify the time (in milliseconds) that Modbus TCP EDS adapter waits for a pending request before marking it as timeout and dropping the request. The default value is 10000 ms. The value must be a positive integer, there is no value range.|
|**DelayBetweenRequests**   | Optional          |number|Parameter to specify the minimum time (in milliseconds) between two successive requests sent to the data source. The value ranges from 0 ms to 1000 ms. The default value is 0 ms.|
|**MaxResponseDataLength**  | Optional          |number    |Parameter to limit the maximum length (in bytes) of data that can be read within one transaction. This feature is provided to support devices that limit the number of bytes that can be returned. If there is no device limitation, the request length should be the maximum length of 250 bytes. The value ranges from 2 to 250. The default value is 250 ms.|


## Modbus TCP data source example

The following is an example of valid Modbus TCP data source configuration:

```json
{
    "IpAddress": "117.23.45.110",
    "Port" : 502,
    "ConnectTimeout" : 10000,
    "StreamIdPrefix" : "DataSource1",
}
```
