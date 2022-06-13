
1. Create a namespace for 2 application  i.e. Python flask and mondodb.
2. Both applications should accessible to each other.
3. Write healthcheck probe and readiness probe for both the application.
4. MongoDB data should should store in persistent volume.
5. Only python flask application should accessible outside the cluster.



# docker login
# docker build -t aj5002/tasksapp-python:1.0 .
# docker commit 875423f77baa aj5002/tasksapp-python:1.0
# docker push aj5002/tasksapp-python:1.0
 - > 1.0: digest: sha256:3c1f59ff8e1c0cfea75361a10b7014737bdaca10f0593fbc42e80e4ca73ef34e size: 1998
# docker images
# docker system prune
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images
  - all dangling build cache

# docker network create tasksapp-net
# docker run --name=mongo --rm -d --network=tasksapp-net mongo
# docker run --name=tasksapp-python --rm -p 5000:5000 -d --network=tasksapp-net aj5002/tasksapp-python:1.0 
# docker ps

# kubectl scale deployment tasksapp --replicas=3

# kubectl apply -f mongo-svc.yaml --namespace=minitask
# kubectl apply -f taskapp-svc.yaml --namespace=minitask

# kubectl get all -o wide --namespace=minitask


# kubectl exec -it tasksapp-7fccdf5bd8-nn6q5 -- /bin/sh
# kubectl exec -it --namespace=minitask tasksapp-7fccdf5bd8-4wwd5 -- /bin/sh


# apk --no-cache add curl
curl 10.111.198.130:27017
## Default namespace ##
172.17.0.6:5000     tasksapp-7fccdf5bd8-rx6f7  ->>apptask 
172.17.0.2          tasksapp-7fccdf5bd8-nn6q5
172.17.0.10         tasksapp-7fccdf5bd8-mn65n
172.17.0.5          mongo-5c975797f4-2cg5j

## minitask namespace ##
172.17.0.12         tasksapp-5566c5b9fd-q477t
172.17.0.11         tasksapp-5566c5b9fd-t46gv
172.17.0.9          tasksapp-5566c5b9fd-w55kf
172.17.0.8          mongo-5c975797f4-tcwpt


# minikube service tasksapp-svc --namespace=minitask 
# minikube service --url tasksapp-svc --namespace=minitask

# kubectl describe pods tasksapp-5566c5b9fd-q477t --namespace=minitask


-------------
mongo commands
show dbs  --- to list
use test  --- to create
db.table.insert({"name":"Ajay"})  ---to insert
show collections 
db.table.find()  --- to show all inside table





























https://levelup.gitconnected.com/deploy-your-first-flask-mongodb-app-on-kubernetes-8f5a33fa43b4

# minikube addons list
# minikube start --vm-driver = virtualbox

-----------------------------------------------------------------------------

- Liveness probe :
    This is for detecting whether the application process has crashed/deadlocked. If a liveness probe fails, Kubernetes will stop the pod, and create a new one.

- Readiness probe : 
    This is for detecting whether the application is ready to handle requests. If a readiness probe fails, Kubernetes will leave the pod running, but won't send any requests to the pod.

- Startup probe : 
    This is used when the container starts up, to indicate that it's ready. Once the startup probe succeeds, Kubernetes switches to using the liveness probe to determine if the application is alive. This probe was introduced in Kubernetes version 1.16.


---------------

9269fb3b0e32 - container id- py

readinessProbe:
  exec:
    command:
    - cat
    - /tmp/healthy
  initialDelaySeconds: 5
  periodSeconds: 5

  ---------

  readinessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 15
            periodSeconds: 10