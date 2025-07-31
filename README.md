# Ontology Discovery

## Getting started

### Prerequisites

In order to run this project you will need python version 3.11 installed on your machine.

The project uses packages from the JFrog repository. To use the packages, you need to export the following environment
variable:

```bash
$ export PIP_EXTRA_INDEX_URL="https://<JFROG_USERNAME>:<JFROG_PASSWORD>@aisera.jfrog.io/artifactory/api/pypi/ds-common/simple"
```

**Note**: You can find `<JFROG_USERNAME>` and `<JFROG_PASSWORD>` in 1Password by searching for "aisera jfrog".

Configure the aws cli:

```bash 
$ aws configure
```

### Setup environment

Clone repository:

```bash
$ git clone git@github.com:Aisera/ontology-discovery.git
$ cd ontology-discovery
```

Create and activate a virtual environment:

```bash
$ virtualenv -p python3.11 venv
$ . ./venv/bin/activate
```

Install the project dependencies:

```bash
$ pip install -e .
```

Copy the `.env.sample` file to `.env` and fill in the values for the environment variables.

```bash
$ cp .env.sample .env
```

Export the environment variables:

```bash
$ export $(grep -v '^#' .env | xargs -0)
```

Connect to the VPN and setup kubectl in the correct environment.

```bash 
$ kubectx <dev_cluster> 
$ kubens <dev_env_name> 
```

Port forward the required services (RDS and KGNER):

```bash 
$ kubectl port-forward service/rds-tunnel 3306
$ kubectl port-forward service/kgner-model-grpc-service 50051
```

## Testing

Install pytest and run the tests, using the following command:

```bash
$ pip install pytest
$ pytest
```

## Features

### Offline

```bash
ontology-discovery pipeline discovery
```

For local testing:

Port forward from mariadb:
```bash
kubectl port-forward service/mariadb 3306
```
Port-forward LLM-Gateway:
```bash
kubectl port-forward svc/llm-gateway 7010
```

Port-forward KGNER:
```bash
kubectl port-forward service/kgner-model-grpc-service 50051
```
