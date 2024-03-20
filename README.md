# How to deploy the microservice demo

This is a basic voting application to show how kubernetes microservices work. You will be able to see the difference between creating and managing the application as Pods, and as a Deployment. This is meant to show the ease in scalability with Deployments versus when you create Pods.

![Architecture Overview](/images/architecture.excalidraw.png)

## Deployment Warning
Please note, this is just a basic default example container of a voting app. It should not be left exposed to the internet because it has clear text username/passwords for the Postgres DB for it to function within the manifest files (a huge no-no). This is so it will work with the Python app that makes up the `voting-app` Pods. 

Be smart with the deployment testing.

## Commands to deploy and check status

Deploying can be done with a single command if you are in the directory with all of the `yaml` files.

From within either the `pod-files` or the `deployment-files` directory run

``` shell
kubectl create -f .
```

## Getting Status of what was created

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

You can reach the `voting-app` and `results-app` frontends by going to the IP address of the Node and the ports `30004` and `30005`

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
