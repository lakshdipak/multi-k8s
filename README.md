# multi-k8s
This is a react application
<br/>Here are the steps to build the application locally and deploy on locally installed Kubernetes cluster. 
1. Install docker; follow docker installation guide https://docs.docker.com/install/
2. Install the minikube to set up kubernetes cluster; follow the link https://kubernetes.io/docs/setup/minikube/#installation
3. Following steps to deploy all the application in kubernetes cluster.
  <br/>change to the complex directory inside your workspace
  <br/><i>$cd complex</i>
  <br/> To avoid adding plain text password in yaml file to connect with posgtres, use below command which creates secret in kubernetes and can be accessed at run time by services.
 <br/>Command Create a secret to store confidencial data like password
 <BR/><i>$kubectl create secret <type-of-secret> <secret-name> --from-literal key=value (key value pair of the secret information)</i>
  <br/><i>$kubectl create secret generic pgpassword --from-literal PGPASSWORD=12345678</i>
  <br/>To list the available secrets
  <br><i>$kubectl get secrets</i>
  <br/>run kubectl to deploy the application you can deploy application one by one or you can deploy all application by giving the directory path of deployment yaml files. In my case it is k8s in side complex folder.
  <br/><i>$kubetcl apply –f  k8s/</i>
  <br/>Above command should return saying changes applied in multiple lines for each deployment and ClusterIPService.
4. Now application has been deployed to kubernetes cluster but not accessible for outside cluster. 
  <br/>To access from outside world we will   deploy an ingress-nginx controller to access application for outside world and manage routing and load balancing. 
  <br/>If you are interested in reading more about nginx follow the link https://kubernetes.github.io/ingress-nginx/deploy/
5. Let’s deploy the ingress nginx to access our application form web browser.
  <br/>Run the following command 
  <br><i>$kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml</i>
  
6. And enable the ingress-nginx to be accessible from web browser use below command.
  <br/><i>$minikube addons enable ingress</i>

7. Now check the ip of exposed nginx with below command
  <br/><i>$minikube ip </i>
  <br/>Copy the ip and paste in the browser and page should be loaded. If you get a security pop-up pl accept and certify.
