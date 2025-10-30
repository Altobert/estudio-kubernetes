# Workloads - Cargas de Trabajo

## 📋 Contenido

### 1. Pods
- Unidad más pequeña desplegable
- Pod lifecycle
- Init containers
- Sidecar containers
- Multi-container patterns

### 2. ReplicaSet
- Mantiene un número estable de réplicas
- Self-healing
- Rara vez usado directamente

### 3. Deployments
- Gestión declarativa de ReplicaSets
- Rolling updates
- Rollbacks
- Scaling
- Estrategias de despliegue

### 4. StatefulSets
- Para aplicaciones con estado
- Identidades de red estables
- Almacenamiento persistente
- Orden garantizado de despliegue

### 5. DaemonSets
- Ejecuta un Pod en cada Node
- Casos de uso: logging, monitoring, storage
- Node selectors

### 6. Jobs
- Tareas que se ejecutan hasta completarse
- Paralelismo
- Backoff limit
- TTL para Jobs finalizados

### 7. CronJobs
- Jobs programados
- Sintaxis cron
- Gestión de ejecuciones

## 🎯 Comandos Esenciales

```bash
# Pods
kubectl run nginx --image=nginx
kubectl get pods -o wide
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- /bin/bash

# Deployments
kubectl create deployment nginx --image=nginx --replicas=3
kubectl scale deployment nginx --replicas=5
kubectl rollout status deployment nginx
kubectl rollout undo deployment nginx

# StatefulSets
kubectl get statefulsets
kubectl scale statefulset <name> --replicas=3

# DaemonSets
kubectl get daemonsets -A

# Jobs
kubectl create job test --image=busybox -- echo "Hello"
kubectl get jobs
kubectl logs job/<job-name>

# CronJobs
kubectl create cronjob hello --image=busybox --schedule="*/1 * * * *" -- echo "Hello"
kubectl get cronjobs
```

## 📝 Ejemplos de YAML

Ver archivos de ejemplo en este directorio.

## 📚 Recursos

- [Workloads](https://kubernetes.io/docs/concepts/workloads/)
- [Pods](https://kubernetes.io/docs/concepts/workloads/pods/)
- [Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

## ✅ Checklist

- [ ] Crear y gestionar Pods
- [ ] Trabajar con Deployments
- [ ] Entender StatefulSets
- [ ] Configurar DaemonSets
- [ ] Crear Jobs y CronJobs
- [ ] Realizar rolling updates
- [ ] Hacer rollbacks
