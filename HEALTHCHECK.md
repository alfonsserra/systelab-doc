# Health Check

Every application should be able to find out very easily whether is healthy or not. 

Implementing a simple health-check API will allow you to do just that.

## Why do we need it?
There are several uses cases where this make sense:
- Kubernetes uses liveness probes to know when to restart a Container. For example, liveness probes could catch a deadlock, where an application is running, but unable to make progress. Restarting a Container in such a state can help to make the application more available despite bugs.
- Kubernetes uses readiness probes to know when a Container is ready to start accepting traffic. A Pod is considered ready when all of its Containers are ready. One use of this signal is to control which Pods are used as backends for Services. When a Pod is not ready, it is removed from Service load balancers.
- A Load balancer distributing traffic to your application or a service discovery (a registry that among other things may periodically checks health of the application hosts) uses liveness probes to be sure that an application running on a specific host will be unable to serve traffic when it’s unhealthy. If found unhealthy, a load balancer may take that host running the application out of rotation, or in case of a service discovery, web service query using DNS will omit the unhealthy host.

