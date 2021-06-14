# IOS-XR Telemetry Configuration

- [IOS-XR Telemetry Configuration](#ios-xr-telemetry-configuration)
  - [PCC Routers Configuration](#pcc-routers-configuration)
  - [SRPCE Configuration](#srpce-configuration)

## PCC Routers Configuration

Show Telemetry Configuration

```console
RP/0/RP0/CPU0:xr9kv-3#show running-config telemetry model-driven 
Mon Jun 14 11:16:22.598 UTC
telemetry model-driven
 destination-group docker-server
  address-family ipv4 10.58.50.220 port 57001
   encoding self-describing-gpb
   protocol grpc no-tls
  !
 !
 sensor-group pcc
  sensor-path Cisco-IOS-XR-infra-xtc-agent-oper:xtc/policy-summary
  sensor-path Cisco-IOS-XR-infra-xtc-agent-oper:xtc/topology-summaries/topology-summary
  sensor-path Cisco-IOS-XR-infra-statsd-oper:infra-statistics/interfaces/interface/latest/generic-counters
 !
 sensor-group optics
  sensor-path Cisco-IOS-XR-controller-optics-oper:optics-oper/optics-ports/optics-port/optics-info
 !
 sensor-group system
  sensor-path Cisco-IOS-XR-wdsysmon-fd-oper:system-monitoring/cpu-utilization
  sensor-path Cisco-IOS-XR-nto-misc-oper:memory-summary/nodes/node/summary
 !
 sensor-group routing
  sensor-path Cisco-IOS-XR-clns-isis-oper:isis/instances/instance/statistics-global
  sensor-path Cisco-IOS-XR-clns-isis-oper:isis/instances/instance/levels/level/adjacencies/adjacency
  sensor-path Cisco-IOS-XR-ipv4-bgp-oper:bgp/instances/instance/instance-active/default-vrf/process-info
  sensor-path Cisco-IOS-XR-ip-rib-ipv4-oper:rib/vrfs/vrf/afs/af/safs/saf/ip-rib-route-table-names/ip-rib-route-table-name/protocol/isis/as/information
 !
 sensor-group interface
  sensor-path openconfig-interfaces:interfaces/interface/state
  sensor-path Cisco-IOS-XR-infra-statsd-oper:infra-statistics/interfaces/interface/data-rate
 !
 subscription pcc
  sensor-group-id pcc sample-interval 10000
  destination-id docker-server
  source-interface Loopback0
 !
 subscription system
  sensor-group-id system sample-interval 10000
  destination-id docker-server
  source-interface Loopback0
 !
 subscription interface
  sensor-group-id interface sample-interval 10000
  destination-id docker-server
  source-interface Loopback0
 !
!
```

Show Telemetry Summary

```console
RP/0/RP0/CPU0:xr9kv-3#show telemetry model-driven summary 
Mon Jun 14 11:17:54.515 UTC
 Subscriptions         Total:    3      Active:    3       Paused:    0
 Destination Groups    Total:    1
 Destinations       grpc-tls:    0 grpc-nontls:    1          tcp:    0            udp:    0
                      dialin:    0      Active:    1     Sessions:    3     Connecting:    0
 Sensor Groups         Total:    5
 Num of Unique Sensor Paths :   12
 Sensor Paths          Total:   12      Active:    7 Not Resolved:    0
 Max Sensor Paths           : 1000
 Max Containers per path    :   16
 Minimum target defined cadence :   30000
 Target Defined cadence factor  :    2
```

Show Telemetry Sensor Group

```console
RP/0/RP0/CPU0:xr9kv-3#show telemetry model-driven sensor-group pcc
Mon Jun 14 11:17:10.242 UTC
  Sensor Group Id:pcc
    Sensor Path:        Cisco-IOS-XR-infra-xtc-agent-oper:xtc/policy-summary
    Sensor Path State:  Resolved
    Sensor Path:        Cisco-IOS-XR-infra-xtc-agent-oper:xtc/topology-summaries/topology-summary
    Sensor Path State:  Resolved
    Sensor Path:        Cisco-IOS-XR-infra-statsd-oper:infra-statistics/interfaces/interface/latest/generic-counters
    Sensor Path State:  Resolved
```

Show Telemetry Subscription

```console
RP/0/RP0/CPU0:xr9kv-3#show telemetry model-driven subscription pcc
Mon Jun 14 11:19:19.579 UTC
Subscription:  pcc
-------------
  State:       ACTIVE
  Source Interface:       Loopback0(Up 0x60000000)
  Sensor groups:
  Id: pcc
    Sample Interval:      10000 ms
    Sensor Path:          Cisco-IOS-XR-infra-xtc-agent-oper:xtc/policy-summary
    Sensor Path State:    Resolved
    Sensor Path:          Cisco-IOS-XR-infra-xtc-agent-oper:xtc/topology-summaries/topology-summary
    Sensor Path State:    Resolved
    Sensor Path:          Cisco-IOS-XR-infra-statsd-oper:infra-statistics/interfaces/interface/latest/generic-counters
    Sensor Path State:    Resolved

  Destination Groups:
  Group Id: docker-server
    Destination IP:       10.58.50.220
    Destination Port:     57001
    Encoding:             self-describing-gpb
    Transport:            grpc
    State:                Active
    TLS :                 False
    Total bytes sent:     205287799
    Total packets sent:   2862
    Last Sent time:       2021-06-14 11:19:15.119173762 +0000

  Collection Groups:
  ------------------
    Id: 51
    Sample Interval:      10000 ms
    Encoding:             self-describing-gpb
    Num of collection:    318
    Collection time:      Min:     5 ms Max:    25 ms
    Total time:           Min:     5 ms Avg:     7 ms Max:    25 ms
    Total Deferred:       0
    Total Send Errors:    0
    Total Send Drops:     0
    Total Other Errors:   0
    No data Instances:    0
    Last Collection Start:2021-06-14 11:19:14.118050474 +0000
    Last Collection End:  2021-06-14 11:19:14.118056601 +0000
    Sensor Path:          Cisco-IOS-XR-infra-xtc-agent-oper:xtc/policy-summary

    Id: 52
    Sample Interval:      10000 ms
    Encoding:             self-describing-gpb
    Num of collection:    318
    Collection time:      Min:     0 ms Max:     0 ms
    Total time:           Min:     9 ms Avg:    16 ms Max:    52 ms
    Total Deferred:       0
    Total Send Errors:    0
    Total Send Drops:     0
    Total Other Errors:   0
    No data Instances:    318
    Last Collection Start:2021-06-14 11:19:14.118056767 +0000
    Last Collection End:  2021-06-14 11:19:14.118071610 +0000
    Sensor Path:          Cisco-IOS-XR-infra-xtc-agent-oper:xtc/topology-summaries/topology-summary

    Id: 53
    Sample Interval:      10000 ms
    Encoding:             self-describing-gpb
    Num of collection:    318
    Collection time:      Min:    37 ms Max:   137 ms
    Total time:           Min:    38 ms Avg:    52 ms Max:   137 ms
    Total Deferred:       0
    Total Send Errors:    0
    Total Send Drops:     0
    Total Other Errors:   0
    No data Instances:    0
    Last Collection Start:2021-06-14 11:19:14.118071885 +0000
    Last Collection End:  2021-06-14 11:19:14.118119884 +0000
    Sensor Path:          Cisco-IOS-XR-infra-statsd-oper:infra-statistics/interfaces/interface/latest/generic-counters
```

## SRPCE Configuration

Show Telemetry Configuration

```console
RP/0/RP0/CPU0:SRPCE-1#show running-config telemetry model-driven 
Mon Jun 14 11:09:38.140 UTC
telemetry model-driven
 destination-group docker-server
  address-family ipv4 10.58.50.220 port 57001
   encoding self-describing-gpb
   protocol grpc no-tls
  !
 !
 sensor-group pce
  sensor-path Cisco-IOS-XR-infra-xtc-oper:pce-lsp-data/lsp-summary
  sensor-path Cisco-IOS-XR-infra-xtc-oper:pce-lsp-data/tunnel-detail-infos
  sensor-path Cisco-IOS-XR-infra-xtc-oper:pce-topology/topology-summaries/topology-summary
 !
 subscription pce
  sensor-group-id pce sample-interval 10000
  destination-id docker-server
  source-interface GigabitEthernet0/0/0/0
 !
!
```

Show Telemetry Summary

```console
RP/0/RP0/CPU0:SRPCE-1#show telemetry model-driven summary 
Mon Jun 14 11:12:05.033 UTC
 Subscriptions         Total:    1      Active:    1       Paused:    0
 Destination Groups    Total:    1
 Destinations       grpc-tls:    0 grpc-nontls:    1          tcp:    0            udp:    0
                      dialin:    0      Active:    1     Sessions:    1     Connecting:    0
 Sensor Groups         Total:    1
 Num of Unique Sensor Paths :    3
 Sensor Paths          Total:    3      Active:    3 Not Resolved:    0
 Max Sensor Paths           : 1000
 Max Containers per path    :   16
```

Show Telemetry Sensor Group

```console
RP/0/RP0/CPU0:SRPCE-1#show telemetry model-driven sensor-group pce
Mon Jun 14 11:10:19.554 UTC
  Sensor Group Id:pce
    Sensor Path:        Cisco-IOS-XR-infra-xtc-oper:pce-lsp-data/lsp-summary
    Sensor Path State:  Resolved
    Sensor Path:        Cisco-IOS-XR-infra-xtc-oper:pce-lsp-data/tunnel-detail-infos
    Sensor Path State:  Resolved
    Sensor Path:        Cisco-IOS-XR-infra-xtc-oper:pce-topology/topology-summaries/topology-summary
    Sensor Path State:  Resolved
```

Show Telemetry Subscription

```console
RP/0/RP0/CPU0:SRPCE-1#show telemetry model-driven subscription pce 
Mon Jun 14 11:10:52.875 UTC
Subscription:  pce
-------------
  State:       ACTIVE
  Source Interface:       GigabitEthernet0_0_0_0(Up 0x60000000)
  Sensor groups:
  Id: pce
    Sample Interval:      10000 ms
    Sensor Path:          Cisco-IOS-XR-infra-xtc-oper:pce-lsp-data/lsp-summary
    Sensor Path State:    Resolved
    Sensor Path:          Cisco-IOS-XR-infra-xtc-oper:pce-lsp-data/tunnel-detail-infos
    Sensor Path State:    Resolved
    Sensor Path:          Cisco-IOS-XR-infra-xtc-oper:pce-topology/topology-summaries/topology-summary
    Sensor Path State:    Resolved

  Destination Groups:
  Group Id: docker-server
    Destination IP:       10.58.50.220
    Destination Port:     57001
    Encoding:             self-describing-gpb
    Transport:            grpc
    State:                Active
    No TLS                
    Total bytes sent:     2069226
    Total packets sent:   318
    Last Sent time:       2021-06-14 11:10:47.3906000002 +0000

  Collection Groups:
  ------------------
    Id: 7
    Sample Interval:      10000 ms
    Encoding:             self-describing-gpb
    Num of collection:    159
    Collection time:      Min:     2 ms Max:     6 ms
    Total time:           Min:     2 ms Avg:     2 ms Max:     6 ms
    Total Deferred:       0
    Total Send Errors:    0
    Total Send Drops:     0
    Total Other Errors:   0
    No data Instances:    0
    Last Collection Start:2021-06-14 11:10:47.3905994405 +0000
    Last Collection End:  2021-06-14 11:10:47.3905997268 +0000
    Sensor Path:          Cisco-IOS-XR-infra-xtc-oper:pce-lsp-data/lsp-summary
          
    Id: 8 
    Sample Interval:      10000 ms
    Encoding:             self-describing-gpb
    Num of collection:    159
    Collection time:      Min:     1 ms Max:    12 ms
    Total time:           Min:     2 ms Avg:     2 ms Max:    13 ms
    Total Deferred:       0
    Total Send Errors:    0
    Total Send Drops:     0
    Total Other Errors:   0
    No data Instances:    0
    Last Collection Start:2021-06-14 11:10:47.3905997312 +0000
    Last Collection End:  2021-06-14 11:10:47.3906000065 +0000
    Sensor Path:          Cisco-IOS-XR-infra-xtc-oper:pce-lsp-data/tunnel-detail-infos
          
    Id: 9
    Sample Interval:      10000 ms
    Encoding:             self-describing-gpb
    Num of collection:    159
    Collection time:      Min:     0 ms Max:     0 ms
    Total time:           Min:     3 ms Avg:     4 ms Max:    15 ms
    Total Deferred:       0
    Total Send Errors:    0
    Total Send Drops:     0
    Total Other Errors:   0
    No data Instances:    159
    Last Collection Start:2021-06-14 11:10:47.3906000108 +0000
    Last Collection End:  2021-06-14 11:10:47.3906004374 +0000
    Sensor Path:          Cisco-IOS-XR-infra-xtc-oper:pce-topology/topology-summaries/topology-summary
```
