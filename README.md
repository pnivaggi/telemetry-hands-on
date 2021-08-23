# Network Telemetry Hands-on

This repo includes technical overview on network telemetry as well as configuration examples to recreate a minimal lab based on Cisco IOS-XR.

## Technical Documentation

- [mdt-intro](docs/mdt-intro.md): introduction to model driven telemetry
- [mdt-protocols](docs/mdt-protocols.md): streaming telemetry protocols (gRPC, gNMI, protobuf) overview]

## Slides

The below slides are used to support the GIN208 lectures at [Telecom ParisTech](https://www.telecom-paris.fr/en/home):

- [GIN208 - MDT APIs Overview](docs/tpt-gin208/GIN208%20-%20MDT%20APIs%20Overview.pdf): Model Driven Telemetry API (data model, serialization, transport protocol) overview
- [GIN208 - MDT XR Config Overview](docs/tpt-gin208/GIN208%20-%20MDT%20XR%20Config%20Overview.pdf): Cisco IOS XR configuration example for MDT dial-out and gNMI dynamic subscriptions

## Telemetry Lab

The demo will be provided during the GIN208 course. However, for those who wish to reproduce the lab and work on telemetry, it is possible thanks to this information:

- [mdt-cli-config-xr](docs/tpt-gin208/mdt-cli-config-xr.pdf): Cisco IOS XR CLI configuration examples for MDT 
- [mdt-gNMI-config-xr](docs/tpt-gin208/mdt-gNMI-config-xr.pdf): Cisco IOS XR MDT configuration example with gNMI
- [mdt-gNMI-subscribe-xr](docs/tpt-gin208/mdt-gNMI-subscribe-xr.pdf): Cisco IOS XR MDT dynamic subscriptions example with gNMI
- [mdt-stack](mdt-docker-stack/README.md): dockerized MDT consumption stack example
- [gnmi-main](gnmi-ipynb/mdt-gNMI-config-xr.ipynb): Jupyter playbook on gNMI config example 
- [gnmi-subscribe](gnmi-ipynb/mdt-gNMI-subscribe-xr.ipynb): Jupyter playbook for gNMI subsciption 