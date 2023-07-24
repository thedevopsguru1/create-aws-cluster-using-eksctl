# create-aws-cluster-using-eksctl
### THIS COMMAND HAS ALL NEEDED TO MAKE SURE PRIVATE EC2 
```
 eksctl create cluster --name test-anael --region us-east-2 --nodegroup-name eboo-nodes --node-type t2.micro --nodes 3 --alb-ingress-access --ssh-public-key anael1 --external-dns-access --ssh-access --node-private-networking
````
### HERE IS THE DESCRIPTION
```
eksctl create cluster --name clustername --region regionhere --nodegroup-name namehere --node-type typehere --node numberofnodes --alb-ingress-access --ssh-public-key keynamehere --external-dns-access --ssh-access
```
### Here is an example for public
```
eksctl create cluster --name test-anael --region us-east-2 --nodegroup-name eboo-nodes --node-type t2.xlarge --nodes 3 --alb-ingress-access --ssh-public-key anael1 --external-dns-access --ssh-access --with-oidc --full-ecr-access
```
### Here is an example for private
```
eksctl create cluster --name test-anael --region us-east-2 --nodegroup-name eboo-nodes --node-type t2.xlarge --nodes 3 --alb-ingress-access --ssh-public-key anael1 --external-dns-access --ssh-access --node-private-networking --with-oidc --full-ecr-access
```
### for more options, add the flag --help at the end of the commands
_________________________________________________________

# Delete-aws-cluster-using-eksctl
```
eksctl delete cluster --name clusternamehere
```
#### For example, 
```
eksctl delete cluster --name test-anael
```
# Add EFS Volume
#### Create EFS volume
#### Follow this guide to add efs to kubernetes cluster
https://github.com/kubernetes-sigs/aws-efs-csi-driver/blob/master/examples/kubernetes/dynamic_provisioning/README.md
##### test it using :
```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: efs-sc
provisioner: efs.csi.aws.com
parameters:
  provisioningMode: efs-ap
  fileSystemId: fs-92107410
  directoryPerms: "700"
  gidRangeStart: "1000" # optional
  gidRangeEnd: "2000" # optional
  basePath: "/dynamic_provisioning" # optional
```
###### Change the  fileSystemId
```
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: efs-claim
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: efs-sc
  resources:
    requests:
      storage: 5Gi
---
apiVersion: v1
kind: Pod
metadata:
  name: efs-app
spec:
  containers:
    - name: app
      image: centos
      command: ["/bin/sh"]
      args: ["-c", "while true; do echo $(date -u) >> /data/out; sleep 5; done"]
      volumeMounts:
        - name: persistent-storage
          mountPath: /data
  volumes:
    - name: persistent-storage
      persistentVolumeClaim:
        claimName: efs-claim
```
