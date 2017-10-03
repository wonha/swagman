# Swagman

## Overview
The goal of Swagman is to create test specification from API specification. Swagman generates [Newman collection](https://www.getpostman.com/docs/postman/collection_runs/command_line_integration_with_newman) file from [Swagger YAML file](https://swagger.io/docs/specification/basic-structure/). Testing your API with auto-generated test specification assures that your API implementation is reflecting it's description documentation.  
Each test request item of generated collection file contains assertion code in Javascript.

## Usage
`swagman` is a Perl script which generates test specification from Swagger YAML. Swagger is the API specification tool.
Run Swagman with Swagger YAML file.
```
$ ./swagman ./samples/swagger.yml
```
This will generate test specification in format of Newman collection file. Number of collection files `*.postman_collection.json` will be created in `./swagman-collections` directory.  
Newman is a command line collection(sequence of request) runner for Postman application. Postman is a REST API test tool. We will use `swagman-runner` to run the collection files instead of directly run on Newman, since Newman doesn't provide globbing feature and dynamic setting of base URL.
Run Newman with generated collection file, and validate your API Implementation.
```
$ ./swagman-runner 'http://localhost:8080' ./swagman-collections/*.postman_collection.json
```
You can run `newman-adviser` with your CI/CD Pipeline using Jenkins or Docker Cloud.  
Sometimes test fixture is required to success the test.
You can customize the order of request with Postman Application easily.
Import your collection file into Postman, and customize your request & test code.
Note that you need to make [environments](https://www.getpostman.com/docs/postman/environments_and_globals/manage_environments) for base URL when using Postman application.
Once the test specification is completed, you can export it to run with `swagman-runner`.

### Prerequisites
##### perl
perl is required to run swagman and swagman-runner.
> for Mac users

No need to install perl by yourself.
> for Windows users

Install Perl
##### Node.js and NPM
Node.js and NPM is required to run newman.
> for Mac users

```
$ brew install node      # Install Node.js and Node Package Manager
$ npm install -g newman  #  Install Newman
```
> for Windows users

##### perl YAML module
YAML module is required to run swagman.
> for Mac users

```
```
> for Windows users

##### (Optional) Postman application
download link

