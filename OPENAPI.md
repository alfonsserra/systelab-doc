# Generate REST Api clients

In order to generate the client for a REST Api specified with OpenApi, use https://github.com/OpenAPITools/openapi-generator. 
Download the jar file from [sonatype](https://oss.sonatype.org/content/repositories/snapshots/org/openapitools/openapi-generator-cli/4.0.0-SNAPSHOT/)

Run the generator with the command:

```bash
java -jar openapi-generator-cli-4.0.0.jar generate -i /Users/aserra/General/swagger-codegen/openapifile.json -g typescript-angular -o /Users/aserra/General/swagger-codegen/output
```

Parameters and its meaning are:

-i <spec file>, --input-spec <spec file> location of the OpenAPI spec, as URL or file (required)            

-g <generator name>, --generator-name <generator name> generator to use (see list command for list)

-o <output directory>, --output <output directory> where to write the generated files (current dir by default)

-t <template directory>, --template-dir <template directory> folder containing the template files

The last one is very usefull because lets you customize the files that the openapi.generator will generate.

The openapi.generator works internally with [mustache](https://mustache.github.io/) templates that you can 
find at [modules/openapi-generator/src/main/resources/"your generator"](https://github.com/OpenAPITools/openapi-generator/tree/master/modules/openapi-generator/src/main/resources).

So, an option is get one file form there, customize it, at use it as your default generator.

> You do not need to redefine all the templates, only the ones you want to change. 

In this folder you will find a template example named [api.service.mustache](https://github.com/systelab/systelab-doc/blob/master/api.service.mustache), that lets you customize 
the service files generated for typescript-angular
