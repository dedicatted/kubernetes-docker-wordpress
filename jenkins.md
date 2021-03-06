## Jenkins configuration

### 1 Step

 - Install Java and Jenkins
 - In Jenkins should install all standart plugins and "Build Authorization Token Root Plugin" (it uses in automaticall deploy),
 
### 2 Setp
 - IAM Role
 - In AWS console select IAM -> Users -> Add users
 - create user jenkins and add permissions AmazonEC2ContainerRegistryFullAccess - AWS Managed policy

### 3 Step
 - Next step depends on how kubernetes claster has been installed
 - If You used on Jenkins machine
```
export KUBERNETES_PROVIDER=aws;
curl -sS https://get.k8s.io | bash
```
 - You need to add kubectl to the PATH using command 
```
export PATH=<path/to/kubernetes-directory>/platforms/linux/amd64:$PATH
sudo chmod +x <path/to/kubernetes-directory>/platforms/linux/amd64/kubectl
```
 - If kubernetes has been installed from another machine You should install kuberctl using next commands
```
curl -O https://storage.googleapis.com/kubernetes-release/release/v1.4.3/bin/linux/amd64/kubectl
chmod +x kubectl
mv kubectl /usr/local/bin/
```
 - and copy a config file from ~/.kube/config in directory where Jenkins will be able to read it(for example /var)
 - ans set permisions 
```
sudo chown jenkins /var/config
```


### 4 Step
Jenkin tuning
 - Mail
 - Insert your Email, Password and SMTP server in Manage Jenkins -> Configure System -> E-mail Notification and in the job insert "E-mail Notification", also should choose "Send e-mail for every unstable build"
 - Autobuild
 - In Jenkins job insert token Build Triggers -> Trigger builds remotely (e.g., from scripts) -> Authentication Token Add create Webhook in GitHub repository with your values, for instance  http://12.34.56.789:8080/buildByToken/buildWithParameters?job="job_name"&token="token_value"
 - And insert your values in Jenkins parameters REGION, ECR_REPO, STACK_NAME, POD, CONFIG, KUBECTL

### Repositories

 - nodejs
https://github.com/dedicatted/kuber-nodejs

 - nginx
https://github.com/dedicatted/kuber-nginx

 - haproxy
https://github.com/dedicatted/kuber-haproxy

 - wordpress
https://github.com/dedicatted/kuber-wordpress



