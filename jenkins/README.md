# install and deploy jenkins using helm

### 1. we need to install helm cuz our cluster is private and no one can access it until bastion so lets start 

```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm

```
### 2. jenkins chart 
#### 2.1 adding jenkins repo
```
helm repo add jenkins https://charts.jenkins.io
helm repo update

```
#### 2.2 pull jenkins chart and untar it
```
helm pull --untar jenkins/jenkins
```

#### 2.3 edit jenkins chart values.yaml
```
vim values.yaml
# edit serviceType and set it LoadBalancer
# edit   installPlugins: versions
# u have two options to set namespace u can add namespaceOverride: jenkins Or use -n with helm install command  
```
#### 3. now install your chart
```
helm install jenkins -n jenkins <chart-path>
```

#### 4. run this command to get 'admin' user password

```
kubectl exec --namespace jenkins -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/additional/chart-admin-password && echo
```
#### 5. run this comand to get jenkins LoadBalancer IP and port btw port num is 8080 by default
```
kubectl get svc -n jenkins -o wide
```
