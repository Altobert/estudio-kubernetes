# Conceptos Básicos de Kubernetes

## 📋 Contenido

### 1. Introducción
- ¿Qué es Kubernetes?
- Problemas que resuelve
- Casos de uso

### 2. Contenedores
- Docker básico
- Imágenes y contenedores
- Registry

### 3. Componentes Principales
- **Cluster**: Conjunto de nodos que ejecutan aplicaciones en contenedores
- **Node**: Máquina (física o virtual) que ejecuta Pods
- **Pod**: Unidad básica de despliegue en Kubernetes

### 4. Conceptos Fundamentales
- Declarative vs Imperative management
- YAML manifests
- kubectl - la herramienta de línea de comandos

## 🎯 Comandos Básicos

```bash
# Ver información del cluster
kubectl cluster-info
kubectl get nodes

# Listar recursos
kubectl get pods
kubectl get services
kubectl get deployments

# Describir recursos
kubectl describe pod <pod-name>
kubectl describe node <node-name>

# Crear recursos
kubectl apply -f <archivo.yaml>
kubectl create deployment <name> --image=<image>

# Eliminar recursos
kubectl delete pod <pod-name>
kubectl delete -f <archivo.yaml>
```

## 📚 Recursos de Aprendizaje

- [Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
- [Conceptos de Kubernetes](https://kubernetes.io/es/docs/concepts/)

## ✅ Checklist de Aprendizaje

- [ ] Entender qué es un contenedor
- [ ] Conocer los componentes de un cluster
- [ ] Comprender qué es un Pod
- [ ] Saber usar kubectl básico
- [ ] Entender manifests YAML
