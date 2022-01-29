---
sort: 2
---

# Kubernetes

## What is Kubernetes?

Open source container orchestration tool. It helps manage containerized applications in different deployment environments.

Features:

- High availability or no downtime
- Scalability or high performance
- Disaster recovery(backup and restore)

## Command

Imperative
```bash
# Create Objects
kubectl run --image=nginx nginx
kubectl create deployment --image=nginx nginx
kubectl expose deployment nginx --port 80

# Update Objects
kubectl edit deployment nginx
kubectl scale deployment nginx --replicas=5
kubectl set image deployment nginx nginx=nginx:1.18

# use yaml files
kubectl create -f nginx.yaml
kubectl replace -f nginx.yaml
kubectl delete -f nginx.yaml
```

Declarative
```bash
kubectl apply -f nginx.yaml
```

Some options

`--dry-run` : By default as soon as the command is run, the resource will be created.

`--dry-run=client`: This will not create the resource, instead, tell you whether the resource can be created and if your command is right.

`-o yaml`: This will output the resource definition in YAML format on screen.

e.g.
```bash
kubectl run nginx --image=nginx --dry-run=client -o yaml
```

selector
```bash
kubectl get pods --selector app=App1
```

### namespace

```bash
 kubectl create namespace blue
 kubectl get namespace
# yaml
 kubectl create namespace green --dry-run -o yaml > green-ns.yaml
 kubectl create -f green-ns.yaml
 kubectl delete namespace xx
```

### config
```bash
 kubectl config view
 kubectl config set-context NAME --cluster=kubernetes xxx
 kubectl config use-context NAME
```

### label
```bash
kubectl get pods --show-labels
kubectl get pods -l <label_name>

# create and change
kubectl label pod <name> key=value
kubectl label pod <name> key=value --overwrite
# check 
kubectl label pod <name> --show-labels
# delete 
kubectl label pod <name> key-
```

### Node Affinity

Node Selector sample:
```yaml
spec:
  containers:
  - name: data_pro
    image: data_pro
  
  nodeSelector:
    size: Large

```

Affinity sample 1:
```yaml
spec:
  containers:
  - name: data_pro
    image: data_pro
    
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: size
            operator: In
            values:
            - Large
```

Affinity sample 2:
```yaml
spec:
  containers:
  - name: data_pro
    image: data_pro
    
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: size
            operator: NotIn
            values:
            - Small
```

### Static pods vs Daemonsets

Static Pods
- created by the kubelet
- Deploy control plane components as static pods
- Both ingnored by the Kube-Scheduler

DaemonSets
- Created by Kube-API server(DaemonSet Controller)
- Deploy Monitoring Agents, Logging Agents on nodes
- Both ingnored by the Kube-Scheduler


#### Get Static Pod Path

```bash
ps -ef |  grep /usr/bin/kubelet
```
e.g.
```plain
root@node01:/var/lib/kubelet#  ps -ef |  grep /usr/bin/kubelet 
root     21172     1  0 07:28 ?        00:00:17 /usr/bin/kubelet --bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf --config=/var/lib/kubelet/config.yaml --network-plugin=cni --pod-infra-container-image=k8s.gcr.io/pause:3.2
root     31913 25115  0 07:40 pts/0    00:00:00 grep --color=auto /usr/bin/kubelet
```

```bash
grep -i staticpod /var/lib/kubelet/config.yaml
```
e.g.
```plain
staticPodPath: /etc/just-to-mess-with-you
```

### Check Node CPU
```bash
kubectl top node --sort-by='cpu' --no-headers | head -1
```

### drain

- kubectl drain은 노드 관리를 위해서 지정된 노드에 있는 포드들을 다른곳으로 이동시키는 명령입니다.
- 우선 새로운 포드가 노드에 스케쥴링 되어서 실행되지 않도록 설정합니다.
- 그리고 나서 기존에 이 노드에서 실행중이던 포드들을 삭제합니다. 이 때 노드에 데몬셋으로 실행된 포드들이 있으면 drain이 실패합니다.
- 데몬셋으로 실행한 포드를 무시하고 진행하려면 `--ignore-daemonsets=true` 옵션을 주고 drain을 하면 됩니다.

```bash
 kubectl get nodes
 kubectl drain node01 --ignore-daemonsets=true

 ```

### kubectl corden
 
 - kubectl cordon은 지정된 노드에 더이상 포드들이 스케쥴링되서 실행되지 않도록 합니다.

```bash
kubectl get nodes
kubectl cordon node01
kubectl uncordon node01
---

## Architecture

`Worker Nodes` refered as "Node"

`kubelet` refered as "node agent"

![kube1](https://github.com/miseon119/whylearn.github.io/blob/master/test_long/folder2/images/kube1.png)

`APP Server` is Entrypoint to K8s cluster.

`Controller Manager` keeps track of what's happening in the cluster.

`Scheduler` ensures Pods placement.

`etcd` Kubernetes backing store.

![kube2](https://github.com/miseon119/whylearn.github.io/blob/master/test_long/folder2/images/kube2.png)

## Main Components

Node: virtual or physical machine.

pod: Abstraction over container, a layer of top of the container  , usually 1 application per Pod.

service: set permanent IP address, Lifecycle of Pod and Service not connected

![kube3](https://github.com/miseon119/whylearn.github.io/blob/master/test_long/folder2/images/kube3.png)

**Deployment** for stateless apps, **StatefulSet** for stateful Apps or Databases.


## Kubernetes Configuration

![kube7](https://github.com/miseon119/whylearn.github.io/blob/master/test_long/folder2/images/kube7.png)


## Master Process
![master_proc](https://github.com/miseon119/whylearn.github.io/blob/master/test_long/folder2/images/master_process.png)


### What is a Namespace ?

- Organize resources in namespaces
- Virtual claster inside a cluster

check:
```bash
$ kubectl get namespace
```

using CLI to create namespace:
```bash
$ kubectl create namespace my-namespace
```

using yaml file to create namespace:
```plain
apiVersion: v1
kind: ConfigMap
metadata:
  name: mongodb-configmap
  namespace: my-namespace
data:
  database_url: mongodb-service
```
#### Why you should use namespace?

- Everything in one Namespace is terrible (e.g. multiple deployments, replicasets, services, configmaps)
- Resource grouped in Namespaces
- Conflicts(e.g. Many teams, sampe application)

![conflict](https://github.com/miseon119/whylearn.github.io/blob/master/test_long/folder2/images/conflict.png)

- Resouce Sharing: Staging and Development
- Resouce Sharing: Blue/Green Deployment
- Access and Resource limits on Namespaces

Note:

- Each Namespace must define own ConfigMap


