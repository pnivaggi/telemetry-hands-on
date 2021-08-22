# MDT Consuming Stack

A simple Model Driven Telemetry consuming stack with the required components for ingesting, storing and visualizing telemetry data can be deployed on Docker. The folder mdt-stack of the repo includes all the files needed to setup the stack using docker-compose.yml provided as example.

We are using the following set of Docker containers:

- Telegraf - a collection container that runs the cisco_telemetry_mdt plugin for ingestion of model-driven telemetry data
- InfluxDB - a storage container that runs a time series database which stores the data
- Chronograf, Grafana - visualization containers that runs a web application which allows the exploration of data

The collector listens on port specified in the configuration files for incoming connections. IOS XR will initiate the connection, dialling out to the collector. After the connection establishment, the device will begin to stream data over gRPC to the collector which will send it to a database named telemetry.

Please refer to the following references for details about the three components and the ingestion of telemetry data:

[InfluxData](https://www.influxdata.com/)
- [Input plugin for Model-driven telemetry over gRPC](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/cisco_telemetry_mdt)  
- [Input plugin for Model-driven telemetry over gNMI](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/gnmi)
