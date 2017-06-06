# kubernetes-fluentd-elastic-kibana-cluster
Kubernetes log analysis using Fluentd, Elastic and Kibana


#### Follow me on [![alt text][1.1]][1]

### Usage

1. Create elasticsearch master pod which has elasticsearch-master container

```
    $kubectl create -f es-master.yml

```
2. Create service resource elaticsearch with external cloud provider Loadbalancer. This is not recommented for the production. You can use this to test indices in the elaticsearch and node status  

```
    kubectl create -f es-master-svc.yml

```  
```
    kubectl create -f es-client.yml

```
```
    kubectl create -f es-master-client-svc.yml

```  

```  
    kubectl create -f es-master-internal-svc.yml

``` 

```
    kubectl create -f es-date-statefulset.yml

```
```
    kubectl create -f fluentd.yml

```

```
   kubectl create -f  kibana.yml 
   
```

!['o' output](http://i.imgur.com/CcptHnN.png)


[1.1]: http://i.imgur.com/tXSoThF.png (twitter icon with padding)
[1]: http://www.twitter.com/rahulkrishnanra

