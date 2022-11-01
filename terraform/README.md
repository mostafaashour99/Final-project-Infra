# infrastructure info and setup

![1_-yXfoGjebJS0RIwUNzJ6Ig](https://user-images.githubusercontent.com/52250018/199336829-1d104ab7-aa80-4809-9775-b4b3cf8dfea9.png)

#
1. network module content of :
  - two subnets one for gke and another for bastion
  - nat gateway 
  - firewall to allow ssh

2. gke module content of:
  - private container cluster resource with authorize networks configuration
  - node pool with count 3 
3. bastion module for creating a private vm to connect with gke cluster


# to build this infrastructure you need to follow this steps:
### get copy from code by 
```
git clone https://github.com/mostafaashour99/Final-project-Infra.git
```
### build infrastructure
```
cd terraform/
terraform init
terraform apply --var-files prod.tfvars
```
### connect to private GKE cluster through bastion vm
```
gcloud compute ssh management-instance --tunnel-through-iap
gcloud container clusters get-credentials private-cluster --zone us-central1-a
```
## Now go read jenkins Readme file to deploy jenkins using helm
- <a href="../jenkins">Deploy Jenkins on Cluster Using Helm</a>
