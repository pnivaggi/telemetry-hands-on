
# MDT practical with Cisco IOS-XR

## IOS-XR Router Configuration Options

- **Transport**: The router can deliver telemetry data either across using TCP or gRPC over HTTP/2. Some people will prefer the simplicity of a raw TCP socket, others will appreciate the optional TLS encyption that gRPC brings.
- **Session Initiation**: There are two options for initiating a telemetry session. The router can “dial-out” to the collector or the collector can “dial-in” to the router. Regardless of which side initiates the session, the router always streams the data to the collector at the requested intervals. TCP supports “dial-out” while gRPC supports both “dial-in” and “dial-out.”
- **Encoding**: The router can deliver telemetry data in two different flavors of Google Protocol Buffers: Compact and Self-Describing GPB. Compact GPB is the most efficient encoding but requires a unique .proto for each YANG model that is streamed. Self-describing GPB is less efficient but it uses a single .proto file to decode all YANG models because the keys are passed as strings in the .proto.

## MDT Consumption Stack