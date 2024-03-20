# How to deploy the microservice demo

This is a basic voting application to show how microservices work. You will be able to see the difference between creating and managing the application as Pods, and as a Deployment. This is meant to show the ease in management and scalability with Deployments.

![Architecture Overview](/images/architecture.excalidraw.png)

## Deploy the microservice via the pods and services

Deploy the pods in the `pod-files` folder in the following order with their respective service.

Stage one - `voting-pod` `voting-service`

Stage two - `redis-pod` `redis-service`

Stage three - `postgres-pod` `postgres-service`

Stage four - `worker-app`

Stage five - `result-pod` `result-service`

## Commands to deploy and check status

Deployment

You can deploy all of the manifest files with a single command if you are in the directory with all of the `yaml` files.

From within either the `pod-files` or the `deployment-files` directory run

``` shell
kubectl create -f .
```

Check status of `pod-files` version

``` shell
kubectl get pods,service
```

Check status of the `deployment-files` version

```shell
kubectl get pods,service,deployment,rs
```

## View the end result

Navigate to the frontend pages to view the `voting` and `result` paqes

You will find them at `<nodeIP>:<nodePort>`

## Scale up the Deployment

When using the `deployment-files` version you can now scale up and down your number of ReplicaSets for critical pods like the voting frontend.

``` shell
kubectl scale deployment voting-app-deploy --replicas=3
```

Notice at the bottom of the page how the `Processed by container ID` changes constantly as you refresh or change votes repeatedly, as it is now hitting random available Pods

![Example](/images/id.example.png)

## Environment tear down

Because we labeled all pods and services with `demo-voting-app` we can easily teardown the environment with a single command.

``` shell
kubectl delete all --selector=app=demo-voting-app
```

Checking the Pods, Services, Deployments and ReplicaSets should return no trace of the `voting-app`
