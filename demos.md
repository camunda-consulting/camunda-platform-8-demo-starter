# Camunda Platform 8 Demo Starter

## Using Docker Compose to build demos

> :information_source: Docker 20.10.16+ is required.

This project is based on a fork of camunda-platform docker. It extends that project with [docker-compose-demo.yaml](docker-compose-demo.yaml) by adding the executor and loader and modifying Identity. To learn more about the environment read the [README.md](README.md)

The full environment contains these components:
- [Zeebe](http://localhost:26500/) (REST Address http://localhost:8088)
- [Operate](http://localhost:8081/)
- [Tasklist](http://localhost:8082/)
- Connectors
- [Optimize](http://localhost:8083/)
- [Identity](http://localhost:8084/)
- [Web Modeler](http://localhost:8070/)
- [Elasticsearch](http://localhost:9200/)
- [Keycloak](http://localhost:18080/)
- PostgreSQL
- [Executor](http://localhost:9090/) (Custom Web app and API's)
- [Loader](http://localhost:8080/) (Data simulator)


## Demo Environment Self-Managed

### Clone the presales-demo-setup environment and build
>**IMPORTANT:** this is a short term solution. Once we have a repo to store the images this will not be necessary. Though it could make sense to have the presales-demo-setup to customize demos

#### clone the project
```shell
$ git clone https://github.com/camunda/presales-demo-setup.git
```

#### build the project in the local docker repo 
```shell
$ docker build --build-arg DEMO=customer-onboarding -f demos.dockerfile -t camunda-consulting/executor .
```
### Clone the camunda-8-simu environment and build *(only needed if you make changes)*
>NOTE: Unlikely but if you need to make a change to camunda-8-simu also called the `loader` you can build that locally as well 
#### clone the project
```shell
$ git clone https://github.com/camunda-consulting/camunda-8-simu.git 
```
#### build the project in the local docker repo 
```shell
$ docker build --no-cache -f Dockerfile -t camunda-community/loader .
```
### To run Demo environment locally clone this repo and issue the following commands:
```shell
$ https://github.com/camunda-consulting/camunda-platform-8-demo-starter.git 
```
```shell
$ docker login registry.camunda.cloud
```
```
Username: your_username
Password: ******
Login Succeeded
```
#### Change the [.env](.env) file to run your DEMO
```
DEMO=loan-processing
```
#### Add connector secrets to the [connector-secrets.txt](connector-secrets.txt) file
```shell
SENDGRID_DEMO=some_secret_key
```
#### Run the environment also rerun this command if you make a change.
```shell
$ docker compose -f docker-compose.yaml -f docker-compose-web-modeler.yaml -f docker-compose-demo.yaml up -d
```
#### To tear down the whole environment run the following command. If you want to delete everything (including any data you created).

```shell
$ docker compose -f docker-compose.yaml -f docker-compose-web-modeler.yaml -f docker-compose-demo.yaml down -v
```
#### Alternatively, if you want to keep the data run:
```shell
$ docker compose -f docker-compose.yaml -f docker-compose-web-modeler.yaml -f docker-compose-demo.yaml down
```

### Login
You can access Self-Managed apps and log in with the user `demo` and password `demo` 

### Deploy or execute a process
Processes will be auto-deployed by the Executor. You can also deploy processes from Webmodeler if needed.

### Emails
Email will usually be sent through Sendgrid. Make sure to configure the send grid secret in the [connector-secrets.txt](connector-secrets.txt)
Go to [Keeper](https://keepersecurity.eu/vault/#) to get the API key that is used for the secret.

## Troubleshooting

### Submitting Issues
Please submit issue to this repos issue board

### Running on arm64 based hardware
See the troubleshooting in the [README.md](README.md#troubleshooting)