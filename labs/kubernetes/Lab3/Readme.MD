
# kubectl Basics

The common format of a `kubectl` command is:

```shell
kubectl action resource
```

This performs the specified action (like create, describe, or delete) on the specified resource (like node or deployment). You can use `--help` after the subcommand to get additional info about possible parameters (for example: `kubectl get nodes --help`).

Check that `kubectl` is configured to talk to your cluster by running the following command:

```shell
kubectl version
```

Check that `kubectl` is installed and you can see both the client and the server versions.

To view the nodes in the cluster, run the following command:

```shell
kubectl get nodes
```

You will see the available nodes. Later, Kubernetes will choose where to deploy our application based on Node available resources.

## Deploy an App

Let’s deploy our first app on Kubernetes with the `kubectl apply -f deployment-file` command. We need to provide the deployment-file which is a yaml-based kubernetes api deployment. Use the file `simple-pod.yaml` as deployment-file.

Great! You just deployed your first application by creating a pod. This performed a few things for you:

- Searched for a suitable node where an instance of the application could be run (we have only 1 available node).
- Scheduled the application to run on that Node.
- Configured the cluster to reschedule the instance on a new Node when needed.

To list your pods, use the following command:

```shell
kubectl get pods
```

You will see that there is at least 1 pod running a single instance of your app. The instance is running inside a container on your node.

## View the App

Pods that are running inside Kubernetes are running on a private, isolated network. By default, they are visible from other pods and services within the same Kubernetes cluster but not outside that network. When we use `kubectl`, we're interacting through an API endpoint to communicate with our application.

We will cover other options on how to expose your application outside the Kubernetes cluster later.


Use
```shell
kubectl get pods
```
 to see the running pods. Select the pod you have started before (look at the RUNNING time).
 
Access the pods exposed port by forwarding it to your local machine.
```shell
kubectl port-forward <pod-name> <target port on your machine>:<exposed port on container>
```

Now, we have a connection between our host (the terminal) and the Kubernetes cluster. The port forward enables direct access to the API from these terminals.

Use curl oder your web browser to validate that the pod is running.
For curl, we can query the endpoint of our application with the command:

```shell
curl http://localhost:<target port on your machine>
```

You can also investigate the running pod with the follwing commands
```shell
kubectl describe pod <pod name>
kubectl logs <pod name>
```

You can also exec into the pod (analogous to docker) by using

```shell
kubectl exec --stdin --tty <pod-name> -- sh
```
