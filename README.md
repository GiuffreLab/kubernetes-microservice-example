# How to deploy the microservice demo

This is a basic voting application to show how microservices work

![Architecture Overview](architecture.excalidraw.png)

## Deploy all of the pods and services

Deploy the pods in the following order with their respective service.

`voting-pod`

`redis-pod`

`postgres-pod`

`worker-app`

`result-pod`

## Commands to deploy and check status

Deployment

``` shell
kubectl create -f <app/service_name>
```

Check status of Pod and Service

``` shell
kubectl get pods,service
```

## View the end result

Navigate to the frontend pages to view the `voting` and `result` paqes

You will find them at `<nodeIP>:<nodePort>`
