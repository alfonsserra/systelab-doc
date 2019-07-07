# Application configuration
Application configuration is everything that is likely to vary between deploys (staging, production, developer environments, etc), including, but not only:

- Resource handles to the database and other backing services.
- Credentials to external services.
- Per-deploy values.

Apps sometimes store config as constants in the code. This is a violation of twelve-factor, which requires strict 
separation of config from code. Config varies substantially across deploys, code does not.

## Design Considerations
You can use properties files, YAML files, environment variables, command-line arguments or an external configuration server.
Usually the application enables more than one options and difines a priority policy.

When using a Config Server, the most advanced solution, the client will consume the configuration on startup and then refresh the configuration without restarting the client to externalize configuration. There are several options like [HashiCorp Consul](https://www.consul.io/configuration.html) or [Spring Cloud Config Server](https://cloud.spring.io/spring-cloud-config/multi/multi__spring_cloud_config_server.html).


