# Example

In this example we deploy the NGINX Ingress Controller (edge) as a [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) using the NGINX Ingress Operator for NGINX Open Source.

## Prerequisites

Have the NGINX Ingress Operator deployed in your cluster. Follow [installation](../../README.md#installation) steps.

## Running the example

1. Create a new namespace for our Ingress Controller instance:
    ```
    kubectl create -f ns.yaml
    ```  

2. Create a new NginxIngressController resource that defines our NGINX Ingress Controller instance (**Note**: If using Openshift, change the `image.tag` to `edge-ubi`):
    ```
    kubectl create -f nginx-ingress-controller.yaml
    ```

 

This will deploy an NGINX Ingress Controller instance using a [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) in the `my-nginx-controller` namespace. 

3. Check if all resources were deployed:

    ```
    kubectl -n my-nginx-ingress  get all
    
    NAME                                               READY   STATUS    RESTARTS   AGE
    pod/my-nginx-ingress-controller-666854fb5f-f67fs   1/1     Running   0          3s
    
    NAME                                  TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
    service/my-nginx-ingress-controller   NodePort   10.103.105.52   <none>        80:30298/TCP,443:32576/TCP   3s
    
    NAME                                          READY   UP-TO-DATE   AVAILABLE   AGE
    deployment.apps/my-nginx-ingress-controller   1/1     1            1           4s
    
    NAME                                                     DESIRED   CURRENT   READY   AGE
    replicaset.apps/my-nginx-ingress-controller-666854fb5f   1         1         1       4s
    ```

For more information about how to configure the NGINX Ingress Controller, check the official [documentation](https://docs.nginx.com/nginx-ingress-controller/overview/).

## Remove

1. Delete the NginxIngressController:
    ```
    kubectl delete -f nginx-ingress-controller.yaml
    ``` 

1. Delete the namespace:
    ```
    kubectl delete namespace my-nginx-ingress
    ```