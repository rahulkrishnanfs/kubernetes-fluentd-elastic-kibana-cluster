# kubernetes-fluentd-elastic-kibana-cluster
Kubernetes log analysis using Fluentd, Elastic and Kibana


#### Follow me on [![alt text][1.1]][1]

### Usage

1. Create elasticsearch master pod which has elasticsearch-master container.

```
    $kubectl create -f es-master.yml
```

2. Create K8s service resource named elasticsearch with external cloud provider Loadbalancer. This is not recommented for the production. You can use this to test indices in the elaticsearch and the node status.  

```
    $kubectl create -f es-master-svc.yml
```

3. Create the slave node to include in the cluster. Check the status of the master and slave node with the help of following url.

```
    http://< serverip >:9200/_cat/nodes
```


4. Create a Deployment resource named elasticsearch-client with container named elasticsearch-client. This will be added as a slave node
   in the cluster. 

```
    kubectl create -f es-client.yml
```

5. Create a K8s service named elastic-discovery with port 9300 port for syncing the cluster 

```
   kubectl create -f es-master-client-svc.yml
```

6. Create a service named elasticsearch-internal, so that services can make use of elasticsearch cluster. This service is not exposing to the outside world .

```
    kubectl create -f es-master-internal-svc.yml
```

 7. This will create a pod to store data in the elasticsearch cluster with the help of Statefulsets kubernetes resource. 
 
```
    kubectl create -f es-date-statefulset.yml
```
    
    
 !['o' output](http://i.imgur.com/WjMNfy0.png)


8. Fluentd pod is deployed across the K8s cluster using Deployment resource. This will ensure that a copy of Fluend pod is running on all minions

```
    kubectl create -f fluentd.yml
```

9.  Kibana pod will be created and accessing the logs by communicating the elasticsearch cluster using the elasticsearch-internal service with 9200 port.

```
    kubectl create -f  kibana.yml 
 ``` 
 
 10. Kibana K8s service will be created with external cloud provider Loadbalancer to access the kinana using port 5601

```
    kubectl create -f  kibana-svc.yml 
 ``` 

!['o' output](http://i.imgur.com/CcptHnN.png)



[1.1]: http://i.imgur.com/tXSoThF.png (twitter icon with padding)
[1]: http://www.twitter.com/rahulkrishnanra


### Useful kubectl commands to check the status of the ELF cluster 

```
 $kubectl get pods --namespace=< namespace  >
 $kubectl get deployments
 $kubectl get services
 $kubectl get statefulsets

```

##Create a PR if you find any issue. I would welcome you to contribute to this project fast developent 
