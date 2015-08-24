# Activiti Demo

## Usage

Install [Vagrant](https://www.vagrantup.com/downloads.html) first. Clone the project and go into the project directory. Then,

```
vagrant up
```

The VM is configured so that the Activiti application is forwarded to your machine on port 8080.

To check out the activiti-explorer application navigate to [http://localhost:8080/activiti-explorer](http://localhost:8080/activiti-explorer).

To log in, select the user account shown in [2.2 Activiti setup](http://www.activiti.org/userguide/).

### REST API

All calls to the API will be made using the base URL: http://localhost:8080/activiti-rest/service.

Three things to keep in mind when using the REST API:

1. Always set the Accept header to "application/json"
2. Always set the Content-Type header to "application/json"
3. Always use Basic Authentication

So if you're taking the API for a test drive using cURL, your sample request will look something like this:

```
curl -H "Content-Type: application/json" \
     -H "Accept: application/json" \
     http://yourusername:yourpassword@localhost:8080/activiti-rest/service/repository/deployments
```
