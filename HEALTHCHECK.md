# Health Check

Every application should be able to find out very easily whether is healthy, e.g. is running well, or not. 

Implementing a simple health-check API will allow you to do just that.

## Why do we need it?
There are several uses cases where this make sense:
- Kubernetes uses liveness probes to know when to restart a Container. For example, liveness probes could catch a deadlock, where an application is running, but unable to make progress. Restarting a Container in such a state can help to make the application more available despite bugs.
- Kubernetes uses readiness probes to know when a Container is ready to start accepting traffic. A Pod is considered ready when all of its Containers are ready. One use of this signal is to control which Pods are used as backends for Services. When a Pod is not ready, it is removed from Service load balancers.
- A Load balancer distributing traffic to your application or a service discovery (a registry that among other things may periodically checks health of the application hosts) uses liveness probes to be sure that an application running on a specific host will be unable to serve traffic when it’s unhealthy. If found unhealthy, a load balancer may take that host running the application out of rotation, or in case of a service discovery, web service query using DNS will omit the unhealthy host.

## Design Considerations
It is usually implemented as an API endpoint (e.g. HTTP /health) that returns the health of the service. The API endpoint handler could perform various checks, such as

- the status of the connections to the infrastructure database
- the status of the host resources, e.g. disk space
- application specific logic

Health-check endpoints are called frequently and within fixed intervals, therefore your latencies should ideally be small. 
It’s not intended (although could be used) as a monitoring solution for human operators.

## Implementations

Check [MicroProfile Health](https://microprofile.io/project/eclipse/microprofile-health) and [Springboot Actuator Health](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-endpoints.html#production-ready-health)

For .NET check [ASP.NET Core built-in health monitoring](https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/implement-resilient-applications/monitor-app-health)
