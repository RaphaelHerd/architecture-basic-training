
# kubectl Basics

Ensure that the resources of the old labs are removed/deleted. 
Deploy the service and the pod by using

```shell
kubectl apply -f hpa.yaml
```

Validate the state of the Kubernetes Deployment and the Service by using the learned techniques.

Ensure the HPA is setup correctly by using

```shell
kubectl get hpa
```

Please note that the current CPU consumption is 0% as there are no clients sending requests to the server (the `TARGET` column shows the average across all the Pods controlled by the corresponding deployment).

If the `TARGET` column shown `unknown` as current status, we have to wait a little bit longer until the first metrics are arrived at the HPA.

# Generate Load

When the HPA shows a number >= 0%, the metrics have successfully arrived at the HPA. Now we can generate load in oder to validate the scaling policy.

We can generate load inside Kubernetes itself by simply starting a Pod and requesting the deployed Service.

Before we start, open another console and watch the HPA by using 
```shell
kubectl get hpa -w
```
Switch back to your working console and execute a pod which is generating load by using
```shell
kubectl run -i --tty --rm --image=busybox:1.28 --restart=Never load-test -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://nginx-service; done"
```
You should see the source code of the nginx welcome screen. 

Switch to the new console and watch the HPA load. When the load has passed your limit you have defined in the HPA deployment (averageUtilization attribute), more pods will be added.

You can validate that by watching column `REPLICAS` on the HPA resource or by simply executing `kubectl get pods`.