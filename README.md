# multi-k8s
This is a react application
Here are the steps to build the application locally and deploy on locally installed Kubernetes cluster. 
1. Install docker; follow docker installation guide https://docs.docker.com/install/
2. Install the minikube to set up kubernetes cluster; follow the link https://kubernetes.io/docs/setup/minikube/#installation
3. Following steps to deploy all the application in kubernetes cluster.
  <br/>change to the complex directory inside your workspace
  <br/><i>$cd complex</i>
  <br/>run kubectl to deploy the application you can deploy application one by one or you can deploy all application by giving the directory path of deployment yaml files. In my case it is k8s in side complex folder.
  <br/><i>$kubetcl apply –f  k8s/</i>
  <br/>Above command should return saying changes applied in multiple lines for each deployment and ClusterIPService.
4. Now application has been deployed to kubernetes cluster but not accessible for outside cluster. 
  <br/>To access from outside world we will   deploy an ingress-nginx controller to access application for outside world and manage routing and load balancing. 
  <br/>If you are interested in reading more about ngnix follow the link https://kubernetes.github.io/ingress-nginx/deploy/
5. Let’s deploy the ingress nginx to access our application form web browser.
  <br/>Run the following command 
  <br><i>$kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml</i>
  
  <br/>And enable the ingress-nginx to be accessible from web browser use below command.
  <br/><i>$minikube addons enable ingress</i>

  <br/>Now check the ip of exposed ngnix with below command
  <br/><i>$minikube ip </i>
  <br/>Copy the ip and paste in the browser and page should be loaded. If you get a security pop-up pl accept and certify.
