# External configuration
An app’s config is everything that is likely to vary between deploys (staging, production, developer environments, etc). 
This includes:

- Resource handles to the database, Memcached, and other backing services
- Credentials to external services such as Amazon S3 or Twitter
- Per-deploy values such as the canonical hostname for the deploy

Apps sometimes store config as constants in the code. This is a violation of twelve-factor, which requires strict 
separation of config from code. Config varies substantially across deploys, code does not.

## Design Considerations
