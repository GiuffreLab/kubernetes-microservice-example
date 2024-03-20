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

You can also deploy all of the manifest files with a single command if you have all of the `yaml` files in a single directory.

From within the directory run

``` shell
kubectl create -f .
```

Check status of Pod and Service

``` shell
kubectl get pods,service
```

## View the end result

Navigate to the frontend pages to view the `voting` and `result` paqes

You will find them at `<nodeIP>:<nodePort>`

## Environment tear down

Because we labeled all pods and services with `demo-voting-app` we can easily teardown the environment with a single command.

``` shell
kubectl delete all --selector=app=demo-voting-app
```

It should return the following

``` shell
pod "voting-app-pod" deleted
pod "redis-pod" deleted
pod "postgres-pod" deleted
pod "worker-app-pod" deleted
pod "result-app-pod" deleted
service "voting-service" deleted
service "redis" deleted
service "db" deleted
service "result-service" deleted
```

Checking the Pods and Services should return no trace of the `voting-app`
