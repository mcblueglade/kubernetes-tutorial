
Kubernetes
=========== 

1. #This will install env to run kubernetes locally on your machine. Just need Docker to run it  
See: https://minikube.sigs.k8s.io/docs/start/ 
See: https://www.youtube.com/watch?v=s_o8dwzRlu4 
Code: https://gitlab.com/nanuchi/k8s-in-1-hour 
 
Minikube running as a Docker container to help run clusters locally: 
Inside Minikube with have Docker to run our application containers : so two layers of Docker 
$brew install minikube  

2. Install Docker Desktop and Launch 

3. Start minikude with Docker driver which creates local kubernetes cluster on our machine: 
$minikube start --driver docker 

4. Get status of the cluster using minikube: 
$minikube status 
minikube 
type: Control Plane 
host: Running 
kubelet: Running 
apiserver: Running 
kubeconfig: Configured 

5. Get node info with built into minikube “kubectl” client: minikube has kubectl (kubernetes-cli) as dependency when installed.  Displays all nodes in the cluster 
$kubectl get node 

6. Creating secrets we can encode the user names and passwords: 
           echo –n mongouser | base64 
           > 4oCTbiBtb25nb3VzZXIK 
           echo –n mongopassword | base64 
           > 4oCTbiBtb25nb3Bhc3N3b3JkCg== 

7. Had to run the following to start app: 
minikube service webapp-service 

|-----------|----------------|-------------|---------------------------| 

| NAMESPACE |      NAME      | TARGET PORT |            URL            | 

|-----------|----------------|-------------|---------------------------| 

| default   | webapp-service |        3000 | http://192.168.49.2:30100 | 

|-----------|----------------|-------------|---------------------------| 

🏃  Starting tunnel for service webapp-service. 

|-----------|----------------|-------------|------------------------| 

| NAMESPACE |      NAME      | TARGET PORT |          URL           | 

|-----------|----------------|-------------|------------------------| 

| default   | webapp-service |             | http://127.0.0.1:59188 | 

|-----------|----------------|-------------|------------------------| 

Which runs on http://127.0.0.1:59188 

8. To stop servers set the replicas to 0: 
     replicas: 0 
    
     apply the yaml: 
    $ kubectl apply -f mongo-config.yaml. // Apply mapconfig 
    $ kubectl apply -f mongo-secret.yaml // Apply secrets 
    $ kubectl apply -f mongo.yaml  // Apply mongo yaml to setup mongo pod: container template + service 
    $ kubectl apply -f webapp.yaml //Apply webapp.yaml to setup webapp pod : container template + service 
 
or  
$kubectl scale --replicas=0 deployment/webapp-deployment 
$kubectl scale --replicas=0 deployment/mongo-deployment 
    
      
9. Useful commands to see whats running and how: 
$ kubectl --help or e.g. $ kubectl get --help 
$ kubectl get node 
$ kubectl get all 
$ kubectl get configmap 
$ kubectl get secret 
$ kubectl describe service webapp-service 
$ kubectl describe pod webapp-service 
$ kubectl describe pod webapp-deployment-9fccd564d 
$ kubectl logs webapp-deployment-9fccd564d-l2qdq 
$ kubectl logs webapp-deployment-9fccd564d-l2qdq –f 
$ kubectl logs mongo-deployment-855b879886-dtz72 –f 
#shows services 
$ kubectl get svc  
 
Get Ip address of where Node service is running to launch webapp, NodePort is accessible on each Worker Node’s IP Address.  
$ minikube ip 
or 
$kubectl get node –o wide 
 
Launch app in browser using: 
http://192.168.49.2:30100/ 
or 
minikube service webapp-service 
