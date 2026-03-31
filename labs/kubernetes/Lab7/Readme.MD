
# kubectl Basics

Ensure that the resources of the old labs are removed/deleted. Make yourself familia with the deployment files of this lab.
Deploy the resources by using

```shell
kubectl apply -f deployment-advanced.yaml
```

Validate that the service, the deployment and the pods are up and running. Use the techniques you have learned in the previous labs.

Before we are able to invoke the service from outside the cluster, we have to validate the ingress settings.
```shell
kubectl get ingress
```

You can see that there is one nginx-ingress rule that is mapped to a single `HOST` with a wildcard `*` path on a single `PORT` to a single `ADDRESS`. 

In the `ADDRESS` column you can see the created LoadBalancer of the Kubernetes Cloud Controller Manager system component.

Since we have a web service deployed, we can use curl or your web browser to access the service by using the `ADDRESS` and `PORT` values from our ingress rule (e.g. if port 80 is used --> `http://k8s-default-nginxing-b8ed082350-2106131487.us-east-1.elb.amazonaws.com`).

We can also add a custom domain name which is identical to a domain name for our website (e.g. RaphaelHerding.de) by using further annotations in the ingress rule. But keep in mind that this is platform specific since the LoadBalancer is outside of Kubernetes and in responsibility of the provider.