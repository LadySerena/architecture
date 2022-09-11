# Observe APIs

## Introduction

We should use OpenTelemetry APIs since that is something a lot of observability systems are now able to talk to. This
would decrease friction of adoption. The other feature of OpenTelemetry is that there is a notion of no-op logs,
metrics, and tracing. This proposal is mainly intended for the workloads running on Aurae (I don't have an easy solution
for the chicken and egg yet)

### Collector Architecture

The [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/) will run as a pod within the aurae runtime (TODO sort out what is actually means)

### API Usage

I think our resources must declare that they can be observed and maybe which "kinds" of observation a given resource
supports.

- observe.Stdout(myPod)
  - gathers logs from a pod's stdout
- observe.Stderr(myPod)
  - gathers logs from a pod's stderr
- observe.Metrics(myPod)
  - ?????
- observe.withContext(ctx).Stdout(myPod)
  - pass the incoming context into the function for passing in a traceid. The context object can have arbitrary key
    value pairs but aurae's observability system will assume nothing is there beyond standard metadata.
