# estudio-kubernetes
material para el estudio de kubernetes

comandos importantes

// se crea un nuevo deployment
kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0

// para exponer
kubectl expose deployment hello-minikube --type=NodePort --port=8080

//
kubectl get services hello-minikube

// acceder al servicio
minikube service hello-minikube