
# kubectl Basics

Deploy the service and the pod by using

```shell
kubectl apply -f deployment.yaml
```

To list your service, use the following command:

```shell
kubectl get services
```

You will see that there is at least 1 service running.



## Validate that the Service is Working

In order to ensure that the service is able to reach the pods, you have to set labels. We have to validate that the service has selected the correct pods. Use

```shell
kubectl describe service <service-name>
```

to see what you have deployed. Especially take a look to the `Endpoints` row and ensure that at least one ip address is included. Compare the ip address of the endpoints row with the ip address of your deployed pod by using

```shell
kubectl get pods -o wide
```

Now use the port forwarding concept from the previous lab in order to ensure that the application is really returning the correct result. Instead of forwarding the port from the pod, use the created service.
Use the following command to forward an internal Kubernetes port to your local machine.
```shell
kubectl port-forward service/<service-name> <target port on your machine>:<exposed port on container>
```

Again, use curl or your browser to validate that the service and pod are working as expected.