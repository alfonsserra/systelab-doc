# Health Check

Every application should be able to find out very easily whether your application is healthy or not, and if it isn’t, 
then it shouldn’t be serving any traffic at all. 

Implementing a simple health-check API will allow you to do just that.

## Why do we need it?
It informs the load balancer distributing traffic to your application or a service discovery (a registry that among other things may periodically checks health of the application hosts) that your application running on a specific host will be unable to serve traffic when it’s unhealthy. If found unhealthy, a load balancer may take that host running the application out of rotation, or in case of a service discovery, web service query using DNS will omit the unhealthy host.
In case of some weird behaviour with the application on a specific host, you could take that host out of rotation manually, so that you can debug the application without having to shut down the process.
