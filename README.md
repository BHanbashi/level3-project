# Saudi Digital Academy level 3 Final Project

This is the final project (level 3 project) of the DevOps bootcamp. The aim of this project is to set up a near production-ready K8S platform hosting the [Weaveworks Shock Shop demo](https://github.com/microservices-demo). The k8s cluster builds, tests in a test environment and deploys the Sock shop demo app.


## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development, testing and deployment purposes.

### Prerequisites

These tools are needed in order to be able to run this project.

[Docker](https://www.docker.com/get-started)
```
Docker Link
```
[k3d](https://k3d.io/)
```
k3d Link
```
[git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git/)
```
git link
```
[Make](https://www.gnu.org/software/make/)
```
make Link
```

### How to Run
- Clone this repo into the target machine (local machine or live environment) (The following commands assumes Debian-based distribution)
```
git clone https://github.com/BHanbashi/level3-project.git
```
- Navigate into the tekton-files directory of this project
```
cd level3-project/tekton-files/
```
- Run "make up"
```
make up
```

the k8s cluster will be created, then the needed namespaces and tools will be installed inside the cluster. Finally, the demo app will be built using docker, released into docker hub as docker images and then e2e tests will start in 'test' environment. If successful, the demo app will be deployed inside the cluster into production environment.

## Running the tests

Unit tests are applied as part of the build process as each micro-service is built using Docker as a Docker image. no manual steps are needed to run unit tests.

### Break down into end to end tests

e2e tests test and verify that the whole [Weaveworks Shock Shop demo](https://github.com/microservices-demo) is fully functional. Furthermore, these tests are the primary condition for the demo app to be deployed into the production environment from the test environment.
