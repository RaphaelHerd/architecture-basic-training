
# kubectl Basics

Ensure that the resources of the old labs are removed/deleted. 
Deploy the service and the pod by using

```shell
kubectl apply -f deployment.yaml
```

Validate the state of the Kubernetes Deployments by using the following command:

```shell
kubectl get deployments
```
For getting detailed information about the deployment, use


```shell
kubectl describe deployment <deployment-name>
```

To list your service, use the following command:

```shell
kubectl get services
```

You will see that there is one nginx-service running. Use the learned kubectl commands from previous labs in order to validate if the service is running. Check if the service has the same number of `Endpoints` as you have specified in your deployment by using the `replicas` property. Validate that all pods are running (`#replicas` pieces).


Compare the ip addresses of the endpoints row with the ip address of your deployed pods by using

```shell
kubectl get pods -o wide
```

Now use the port forwarding from the previous lab in order to ensure that the application is really returning the correct result. Instead of forwarding the port from the pod, use the created service. 

Again, use curl or your browser to validate that the service and pod are working as expected.

# Desired State Control
In order to test the desired state control capabilities of the Kubernetes Deployment, you can delete a Pod manually by `kubectl delete pod <pod-name>`and discover what happens by watching the list of pods `kubectl get pods -w`.
