
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

## Create and Set Your Own Namespace
To avoid conflicts with other participants of the workshop, create your own namespace before you start. Its important that the name of the namespace is unique. You can look into the existing namespaces by using `kubectl get ns`. 

To create your own namespace, use 

```shell
kubectl create namespace <namespace-name>
```

Validate that the namespace exists in kubernetes with the command from above.

In order to simplify the usage with a custom namespace, we set the default namespace of your CLI to your created namespace by using:
```shell
kubectl config set-context --current --namespace=<namespace-name>
```
To verify that the new namespace is set, use `kubectl config view --minify | grep namespace:`.

## Deploy a Sample Pod


```shell
kubectl run <pod-name> --image=ubuntu
```

You will see that there is at least 1 pod of your ubuntu container image. The instance is running inside a container on your node.

Use 
```shell
kubectl get pods
```

to see the running pods of your cluster. Look at the `STATUS` and `RESTARTS` column of the pod. Explore what will happen over time. You can add the `-w` option at the end of the get pods commands to continuously watch.

Delete the deployed pod by using

Use 
```shell
kubectl delete pod <pod-name>
```