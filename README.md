# create-aws-cluster-using-eksctl
### THIS COMMAND HAS ALL NEEDED TO MAKE SURE PRIVATE EC2 
```
 eksctl create cluster --name test-anael --region us-east-2 --nodegroup-name eboo-nodes --node-type t2.micro --nodes 3 --alb-ingress-access --ssh-public-key anael1 --external-dns-access --ssh-access --node-private-networking
````
### HERE IS THE DESCRIPTION
```
eksctl create cluster --name clustername --region regionhere --nodegroup-name namehere --node-type typehere --node numberofnodes --alb-ingress-access --ssh-public-key keynamehere --external-dns-access --ssh-access
```
### Here is an example
```
eksctl create cluster --name test-anael --region us-east-2 --nodegroup-name eboo-nodes --node-type t2.micro --nodes 3 --alb-ingress-access --ssh-public-key anael1 --external-dns-access --ssh-access
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
