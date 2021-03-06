# Prometheus 

Wrappers are a form of middleware that can be used with go-micro services. They can wrap both the Client and Server handlers. 
This plugin implements the HandlerWrapper interface to provide automatic prometheus metric handling
for each microservice method execution time and operation count for success and failed cases.  

This handler will export two metrics to prometheus:
* **go_micro_requests_total**. How many go-miro requests processed, partitioned by method and status.
* **go_micro_request_durations_microseconds**. Service method request latencies in microseconds, partitioned by method.

# Usage

When creating your service, add the wrapper like so.

```go
    service := micro.NewService(
        micro.Name("service name"),
    	micro.Version("latest"),
    	micro.WrapHandler(prometheus.NewHandlerWrapper()),
    )
    
    service.Init()
```

