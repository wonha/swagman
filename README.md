# Swagman

## Overview
The goal of Swagman is to generate test specification from API specification. More specifically, Swagman generates [Newman collection files](https://www.getpostman.com/docs/postman/collection_runs/command_line_integration_with_newman) from given [Swagger YAML file](https://swagger.io/docs/specification/basic-structure/).  
  
Swagman fits well with Test Driven Development. Testing API with auto-generated test specification from API specification can assure that your API implementation is reflecting it's description documentation.

## Dependent tools
- [Postman](https://www.getpostman.com/)
    - Postman is a REST API test tool. You can make/launch collection (sequence of request item) with Postman.
- [Newman](https://www.getpostman.com/docs/postman/collection_runs/command_line_integration_with_newman)
    - Newman is a command line collection runner for Postman application.

## Usage
`swagman` is a Perl script which generates the test specification.

#### Run Swagman
```
$ ./swagman sample_swagger.yml
```
Generated collection files will locate on `./autogen-collections` directory. Each request item in the collection file contains it's assertion code for server response in Javascript syntax.  
When executing collection files, it will be more convenient to use `swagman-runner` instead of directly launch Newman. This is because currently Newman does not support shell's globbing feature and dynamic setting of the server's base URL.

#### Run Swagger runner
```
$ ./swagman-runner 'http://localhost:8080' ./autogen-collections/*.postman_collection.json
```
`swagman-runner` exits with return code which Jenkins can recognize so that the entire Jenkins build can success or fail. You can also use other CI/CD Pipeline include Docker Cloud.  

#### Customize collection file
For large API, test fixture or/and ordering of requests is required to success the use case test. Further, you might want to change test behavior for server response. This customization can be done with Postman application. After customizing, You can export it to collection file again to run with `swagman-runner`.

---
_*Note that you need to make [environments](https://www.getpostman.com/docs/postman/environments_and_globals/manage_environments) for base URL when using Postman application._

### Prerequisites
#### perl
perl is required to run swagman and swagman-runner.
##### for Mac users
No need to install perl by yourself.
##### for Windows users
Install StrauberryPerl or ActivePerl according on your taste.
#### Newman
```
$ npm install -g newman
```
#### perl YAML module
YAML module is required to run swagman.  
  
Check `cpan` is on your system or not. If not, install cpan.
```
$ cpan -version
```
Install YAML module using cpan.
```
$ sudo cpan YAML
```
#### (Optional) Postman application
[Postman Download link](https://www.getpostman.com/)

