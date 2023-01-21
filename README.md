# kojitechs-ci-cd-demo-infra-pipeline-tf

## connect to jenkins server:
```
http://<publicIP>:8080/
```
## Install plugins
Go to `manage jenkins`, `manage plugins` 
- sonarqube scanner 
- slack notification
- Quality Gates
- aws steps

## Edit jenkins bash profile
```
vi ~/.bash_profile

M2_HOME=/opt/maven/apache-maven-3.8.7/bin
PATH=$PATH:$HOME/bin:$M2_HOME
export PATH
```
## make sure you only have java 11 instead java 17
```
openjdk version "17.0.6" 2023-01-17 LTS
OpenJDK Runtime Environment Corretto-17.0.6.10.1 (build 17.0.6+10-LTS)
OpenJDK 64-Bit Server VM Corretto-17.0.6.10.1 (build 17.0.6+10-LTS, mixed mode, sharing)
```
## install java 11
```
sudo yum install java-11-amazon-corretto-headless
sudo yum remove java-17-amazon-corretto-headless
```
## verify make make sure you have java 11
```
java -version
```
## Expect this
```
openjdk version "11.0.18" 2023-01-17 LTS
OpenJDK Runtime Environment Corretto-11.0.18.10.1 (build 11.0.18+10-LTS)
OpenJDK 64-Bit Server VM Corretto-11.0.18.10.1 (build 11.0.18+10-LTS, mixed mode)
```

## configure maven maven on jenkins 
```sh
echo $M2_HOME
/opt/maven/apache-maven-3.8.7
```
## Now go to manage cred
- create a token for sonarqube
- create a token for slack(it's only me!!)





## Sonarqube weebhook
```
http://3.145.169.209:8080/sonarqube-webhook/
```
### jenkins weebhook with github
Setting up webhook configuration for jenkins and github
```hcl
http://174.129.86.6:8080/github-webhook/
```
### Configuring maven 

## Assign shell to jenkins user 
```sh
vi /etc/passwd 
change shell from /bin/fasle to /bin/bash
```
```
maven {
    3.8.1
}
```
### Slack notification
```
slack notification
global configuration
```
### configuring sonarqube server
```
manage plugin
SonarQube ScannerVersion
2.15
Sonar Quality GatesVersion
1.3.1
Blue OceanVersion
1.27.0
```
configure system.
```
SonarQube servers
add SonarQube
name: sonar 
Server URL: http://18.206.246.242:9000
```
3. 
Go to SonarQube server and generate a token 
- sign in
username: admin
password: admin
- Create a jenkins user 
- generate a token

4. 
###  Configure quality Gate
Go to sonarqube server 
- create a webhook 
administration
webhooks
- create webhook
name: jenkins
URL: http://18.205.191.218:8080/sonarqube-webhook/

### Tools to connect with eks cluster 
```
aws-cli 
kubectl
```
## How to connect to eks cluster 
```
aws eks --region us-east-1 update-kubeconfig  --name ci-cd-demo-eks-demo
```
## Troubleshooting
```sh
rm ~/.kube/config

```
# Kubernetes  - PODs
```sh
- managed EKS cluster as the main an Admin using RBAC and kubernetes Role and Role binding to fine-Grain access to the cluster. 
- Using helm to create stable charts release and deploy  applications to EKS cluster
- Setup cloudwatch inside and Data Dog to get inside on application running on the cluster
```