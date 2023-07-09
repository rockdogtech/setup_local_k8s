# setup_local_k8s
A local kubernetes environment setup 

## Pre-requisites

* brew
* Docker for Desktop with k8s enabled
* kafka running locally

## Installation

* install https://developer.confluent.io/quickstart/kafka-local/
* install https://argo-cd.readthedocs.io/en/stable/developer-guide/toolchain-guide/#preface

### Setup kubectl
1) Ensure docker for desktop is running
2) Run the following and/or add to your ~/.zprofile
```bash
kubectl config get-contexts &&\
 kubectl config use-context docker-desktop &&\
 kubectl cluster-info
```

### Setup Kafka
Install confluent kafka

```bash
brew install confluentinc/tap/cli
confluent local kafka start
```

Test kafka installation (producer)

```bash
confluent local kafka topic create test
confluent local kafka topic produce test
```

Test kafka installation (consumer)
```bash
confluent local kafka topic consume test  --from-beginning
```

#### Without Kustomize 

1) create cronjob yaml file
2) Run the following command
```bash
kubectl create -f ./warband/job/cronjob.yml
```

#### Cleanup
```bash
kubectl delete pod $(kubectl get pods | grep Completed | awk '{print $1}')
```

#### Stop Kafka
```bash
confluent local kafka stop
```
