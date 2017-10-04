# Swagman

## Overview
The goal of Swagman is to create test specification from API specification. Swagman generates [Newman collection](https://www.getpostman.com/docs/postman/collection_runs/command_line_integration_with_newman) file from [Swagger YAML file](https://swagger.io/docs/specification/basic-structure/).  
  
Swagman fits well with Test Driven Development. Testing API with auto-generated test specification from API specification can assure that your API implementation is reflecting it's description documentation.

### Dependencies
Newman is a command line collection(sequence of request) runner for Postman application. Postman is a REST API test tool.
collection


## Usage
`swagman` is a Perl script which generates Newman collection file from given Swagger YAML file.

#### Run Swagman
```
$ ./swagman sample_swagger.yml
```
Generated collection files will locate in `./autogen-collections` directory. Each request item in the collection file contains it's assertion code for the response with Javascript code.  
When executing these collections, it will be better to use `swagman-runner` instead of directly launching Newman. This is because currently Newman does not support shell's globbing feature and dynamic setting of base URL.

#### Run Swagger runner
```
$ ./swagman-runner 'http://localhost:8080' ./autogen-collections/*.postman_collection.json
```
`swagman-runner` exits with return code which Jenkins can recognize so that the Jenkins build can success or fail. You can also use other CI/CD Pipeline include Docker Cloud.  

#### Customize collection file
For large API, test fixture or/and ordering of requests is required to success the use case test. Or, you might want to change test behavior for server response. This customizing can be done with Postman application. You can export it to collection file again to run with `swagman-runner`.

---
_*Note that you need to make [environments](https://www.getpostman.com/docs/postman/environments_and_globals/manage_environments) for base URL when using Postman application._

### Prerequisites
#### perl
perl is required to run swagman and swagman-runner.
> for Mac users

No need to install perl by yourself.
> for Windows users

Install StrauberryPerl or ActivePerl according on your taste.
### Newman
```
$ npm install -g newman
```
### perl YAML module
YAML module is required to run swagman.  
Check `cpan` is on your environment or not. If not exists, install cpan.
```
$ cpan -version
```
Install YAML module.
```
$ sudo cpan YAML
```

### (Optional) Postman application
[Postman Download link](https://www.getpostman.com/)

