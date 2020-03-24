[![Circle CI](https://circleci.com/gh/lightstep/opentelemetry-exporter-java.svg?style=shield)](https://circleci.com/gh/lightstep/opentelemetry-exporter-java) [![Apache-2.0 license](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# LightStep OpenTelemetry Exporter

The LightStep OpenTelemetry Exporter is a trace exporter that sends span data to LightStep via OkHttp

```xml
<dependency>
    <groupId>com.lightstep.opentelemetry</groupId>
    <artifactId>opentelemetry-exporter-java</artifactId>
    <version>VERSION</version>
</dependency>
```

## Usage
```java

// Instantiate the exporter
LightStepSpanExporter exporter =
        LightStepSpanExporter.newBuilder()
            .setAccessToken("{your_access_token}")
            .setCollectorHost("{lightstep_host}")
            .setCollectorPort("{lightstep_port}")
            .setCollectorProtocol("{lightstep_protocol}")
            .build();

// Add Span Processor with LightStep exporter
OpenTelemetrySdk.getTracerProvider()
       .addSpanProcessor(SimpleSpansProcessor.newBuilder(exporter).build());
```

## Configuration from system properties and environmental variables

LightStep exporter can be configured by system properties and environmental variables:

* `LS_COLLECTOR_PROTOCOL` - protocol which will be used when sending data to the tracer, `http` or `https`, default is `https`
* `LS_COLLECTOR_PORT` -  port to which the tracer will send data, default is `443`
* `LS_COLLECTOR_HOST` -  host to which the tracer will send data, default is `collector-grpc.lightstep.com`
* `LS_DEADLINE_MILLIS` - maximum amount of time the tracer should wait for a response from the collector when sending a report, default is 30000.
* `LS_COMPONENT_NAME` - name of the component being traced, default is Java runtime command
* `LS_ACCESS_TOKEN` - token for LightStep access

An example of LightStep exporter initialization:
```java
Builder builder = LightStepSpanExporter.Builder.fromEnv();
builder.install();
```

## License

[Apache 2.0 License](./LICENSE).
