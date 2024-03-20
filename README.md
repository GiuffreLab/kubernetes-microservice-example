# How to deploy the microservice demo

This is a basic voting application to show how microservices work. You will be able to see the difference between creating and managing the application as Pods, and as a Deployment. This is meant to show the ease in management and scalability with Deployments.

![Architecture Overview](architecture.excalidraw.png)

## Deploy the microservice via the pods and services

Deploy the pods in the following order with their respective service.

Stage one - `voting-pod` `voting-service`

Stage two - `redis-pod` `redis-service`

Stage three - `postgres-pod` `postgres-service`

Stage four - `worker-app`

Stage five - `result-pod` `result-service`

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
