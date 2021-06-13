# Protobuf, gRPC and gNMI

- [Protobuf, gRPC and gNMI](#protobuf-grpc-and-gnmi)
  - [Google Protocol Buffers (GPB)](#google-protocol-buffers-gpb)
  - [gRPC](#grpc)
  - [gNMI](#gnmi)
  - [References](#references)

---

## Google Protocol Buffers (GPB)

Protocol buffers are a method of serializing data that can be transmitted over wire or be stored in files. Like JSON and XML, the Protobufs are language and platform-neutral. The Protobuf is optimized to be faster than JSON and XML and is making the transmitted data as small as possible. The definition of the data to be serialized is written in configuration files called ***proto files*** (.proto). These files will contain the configurations known as messages. The proto files can be compiled to generate the code in the user's programming language.

Protocol buffers use separation of concerns between context and data.  

Consider a JSON example.
```json
{
  first_name: "Arun",
  last_name: "Kurian"
}
```

In this example, the transmitted data has got an object literal with two properties, `first_name` and `last_name`, with values `Arun` and `Kurian`. This is highly readable, but this can take up more space. Here, every JSON message has to provide both of these pieces every single time. As our data grows, the transmission time will be increased significantly.

But in the case of Protobufs, things are different. We first define a message in a configuration file like this:

```proto
{
  string first_name = 1;
  string last_name = 2;  
}
```

This configuration file contains the context information. The numbers are just identifiers of the fields. By using this configuration, we can send encoded data as

```
124Arun226Kurian
```

In the case of 124Arun, `1` stands for the field identifier, `2` for the data type (which is the string), and `4` is the length of the text. This is a bit more difficult to read than JSON for a human being; however, this will take very little space compared to JSON data. 

---

## gRPC

gRPC is an open-source Remote Procedure Call framework that is used for high-performance communication between services. It is an efficient way to connect services written in different languages with pluggable support for load balancing, tracing, health checking, and authentication. By default, gRPC uses protocol buffers for serializing structured data.

gRPC is based on the **HTTP/2 transport protocol** and it has support for Remote Procedure Calls (RPCs). These are operations that can be called remotely with a set of given parameters and they can return information back to the requestor. The following categories of RPCs exist:

- **Unary RPC** - the client sends a single request to the server and receives a single response back (e.g. polling information).
- **Server streaming RPC** - the client sends a request to get multiple streams of information from the server (e.g. model-driven telemetry); the client can wait for the completion marked in the metadata by the server.
- **Client streaming RPC** - the client sends multiple streams of information to the server; the server typically sends a single response back
- **Bidirectional streaming RPC** - streaming of multiple read-write streams between the client and the server.

In the context of network management, gRPC supports **SSL/TLS authentication**. It is also possible to add custom authentication methods by extending the implementation.

The client uses SSL/TLS authentication to authenticate to the server and to encrypt the messages. There is also an option to use certificates for authentication. The SSL credentials are attached to the gRPC channel.

You define gRPC services in ordinary proto files, with RPC method parameters and return types specified as protocol buffer messages:

```proto
// The greeter service definition.
service Greeter {
  // Sends a greeting
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

// The request message containing the user's name.
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings
message HelloReply {
  string message = 1;
}
```

In the above snippet the `HelloRequest` message definition specifies one field (name/value pair), the `name` data that you want to include in this type of message. The field has a name (here `name` :-) and a type (`string`).  
gRPC uses `protoc` with a special gRPC plugin to generate code from your proto file: you get generated gRPC client and server code, as well as the regular protocol buffer code for populating, serializing, and retrieving your message types.

---

## gNMI

---

## References

<https://grpc.io/>  
<https://developers.google.com/protocol-buffers>  
<https://betterprogramming.pub/understanding-protocol-buffers-43c5bced0d47> 