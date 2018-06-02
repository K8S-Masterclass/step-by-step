# K8S Master Class

* https://portal.eu-central-1.ms.cloudposse.org - Cluster UI Portal
* https://dashboard.portal.eu-central-1.ms.cloudposse.org/#!/overview - K8S Dashboard
* https://grafana.portal.eu-central-1.ms.cloudposse.org/?orgId=1 - Grafana


Clone https://github.com/K8S-Masterclass/step-by-step some where in home directory.

## 1. Install the Geodesic Modules

```
docker run --rm -e DOCKER_TAG goruha/eu-central-1.ms.cloudposse.org:dev | sudo bash -s dev
```

## 2. Run into Geodesic Module Shell

```
eu-central-1.ms.cloudposse.org
```

## 3. Config AWS credentials

Add to `/localhost/.aws/config`

```
[profile k8s-ms]
region=eu-central-1

[profile k8s-ms-user]
region=eu-central-1
role_arn=arn:aws:iam::XXXXXXXXXXXX:role/user
mfa_serial=arn:aws:iam::XXXXXXXXXXXX:mfa/user
source_profile=k8s-ms
```

```
aws-vault add k8s-ms
```

## 4. Assume role

```
assume-role
```

## 5. Export K8S connection configs

```
kops export kubecfg $KOPS_CLUSTER_NAME
```

## 6. Test kubectl connection

```
kubectl get nodes
```

## 7. Create personal namespace

```
kubectl create namespace {}
kubens {}
```

## 8. Create Pod

```
kubectl create -f 2.pod.yaml
kubectl get pods
kubectl logs {}
```

## 9. Create Replica Set

```
kubectl create -f 3.replica_set.yaml
kubectl get pods
kubectl get replicasets
```

## 10. Delete Pod

```
kubectl delete -f 2.pod.yaml
kubectl get pods
kubectl get replicasets
```

## 11. Delete Replica Set

```
kubectl delete -f 3.replica_set.yaml
kubectl get pods
kubectl get replicasets
```

## 12. Create Deployment

```
kubectl create -f 4.deployment.yaml
kubectl get deployment
kubectl get replicasets
kubectl get pods
```

## 13. Create Service

```
kubectl create -f 5.service.yaml
kubectl get services
```

## 14. Create Config Maps

```
kubectl create -f 6.configmaps.yaml
```

Mount configs in deployment

```
kubectl apply -f 4.deployment.yaml
```

## 15. Use Ingress

```
kubectl delete -f 5.service.yaml
```

Set Service type = `ClusterIP`

```
kubectl create -f 5.service.yaml
kubectl create -f 7.ingress.yaml
```
Uncomment Extrnal-DNS

```
kubectl apply -f 7.ingress.yaml
```

## 16. CertBot

Uncomment TLS related

```
kubectl apply -f 7.ingress.yaml
```
