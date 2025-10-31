# Troubleshooting - Resolución de Problemas

## 📋 Contenido

### 1. Debugging de Pods
- Estados de Pods
- Errores comunes
- Estrategias de debugging

### 2. Logs
- Container logs
- Previous container logs
- Multi-container logs
- Logs de componentes del sistema

### 3. Eventos
- Ver eventos del cluster
- Filtrar eventos
- Interpretar eventos

### 4. Diagnóstico de Red
- Conectividad entre Pods
- DNS resolution
- Service endpoints
- Network policies

### 5. Problemas de Recursos
- CPU throttling
- OOMKilled
- Resource limits
- Node pressure

### 6. Problemas de Almacenamiento
- PVC binding issues
- Volume mount problems
- Permissions

## 🎯 Comandos de Debugging

### Información Básica
```bash
# Estado general del cluster
kubectl cluster-info
kubectl get nodes
kubectl top nodes
kubectl get pods --all-namespaces

# Información detallada
kubectl describe pod <pod-name>
kubectl describe node <node-name>
kubectl get events --sort-by='.lastTimestamp'
```

### Logs
```bash
# Logs básicos
kubectl logs <pod-name>
kubectl logs <pod-name> -c <container-name>
kubectl logs <pod-name> --previous
kubectl logs <pod-name> --tail=100
kubectl logs <pod-name> --since=1h
kubectl logs <pod-name> -f

# Logs de múltiples pods
kubectl logs -l app=myapp
kubectl logs deployment/<deployment-name>
```

### Ejecutar Comandos
```bash
# Ejecutar comando en contenedor
kubectl exec <pod-name> -- <command>
kubectl exec <pod-name> -c <container-name> -- <command>

# Shell interactivo
kubectl exec -it <pod-name> -- /bin/bash
kubectl exec -it <pod-name> -- /bin/sh

# Debugging con contenedor temporal
kubectl run debug --image=busybox --rm -it --restart=Never -- sh
kubectl debug <pod-name> -it --image=busybox
```

### Networking
```bash
# Port forwarding
kubectl port-forward <pod-name> 8080:80
kubectl port-forward service/<service-name> 8080:80

# Probar conectividad
kubectl run curl --image=curlimages/curl --rm -it --restart=Never -- sh
kubectl run busybox --image=busybox --rm -it --restart=Never -- sh

# DNS testing
kubectl run -it --rm debug --image=busybox --restart=Never -- nslookup <service-name>
kubectl run -it --rm debug --image=busybox --restart=Never -- wget -O- <service-name>

# Ver endpoints
kubectl get endpoints
kubectl describe service <service-name>
```

### Recursos
```bash
# Uso de recursos
kubectl top nodes
kubectl top pods
kubectl top pods --containers

# Resource quotas y limits
kubectl describe resourcequota
kubectl describe limitrange
```

### Manifests
```bash
# Ver manifests actuales
kubectl get pod <pod-name> -o yaml
kubectl get deployment <deployment-name> -o yaml
kubectl get service <service-name> -o json

# Dry-run y validation
kubectl apply -f manifest.yaml --dry-run=client
kubectl apply -f manifest.yaml --dry-run=server
kubectl diff -f manifest.yaml
```

## 🔍 Problemas Comunes

### Pod en estado Pending
**Causas:**
- Recursos insuficientes
- PVC no puede bind
- NodeSelector no coincide
- Taints y tolerations

**Debug:**
```bash
kubectl describe pod <pod-name>
kubectl get events | grep <pod-name>
kubectl get nodes -o wide
```

### Pod en estado CrashLoopBackOff
**Causas:**
- Error en la aplicación
- ConfigMap o Secret faltante
- Comando incorrecto
- Healthcheck fallando

**Debug:**
```bash
kubectl logs <pod-name> --previous
kubectl describe pod <pod-name>
kubectl get pod <pod-name> -o yaml
```

### Pod en estado ImagePullBackOff
**Causas:**
- Imagen no existe
- Credenciales incorrectas
- Registry no accesible
- Tag incorrecto

**Debug:**
```bash
kubectl describe pod <pod-name>
kubectl get events | grep <pod-name>
```

### Pod en estado Error/Completed
**Debug:**
```bash
kubectl logs <pod-name>
kubectl get pod <pod-name> -o yaml
```

### Servicio no accesible
**Debug:**
```bash
kubectl get service <service-name>
kubectl get endpoints <service-name>
kubectl describe service <service-name>
kubectl get pods -l <service-selector>

# Test desde otro pod
kubectl run test --image=busybox --rm -it --restart=Never -- wget -O- <service-name>:port
```

### Problemas de DNS
**Debug:**
```bash
kubectl get pods -n kube-system -l k8s-app=kube-dns
kubectl logs -n kube-system -l k8s-app=kube-dns

# Test DNS
kubectl run -it --rm debug --image=busybox --restart=Never -- nslookup kubernetes.default
```

### Problemas de almacenamiento
**Debug:**
```bash
kubectl get pv
kubectl get pvc
kubectl describe pv <pv-name>
kubectl describe pvc <pvc-name>

# Ver volúmenes en pod
kubectl describe pod <pod-name> | grep -A 5 Volumes
```

## 🛠️ Herramientas Útiles

- **kubectl debug**: Ephemeral containers para debugging
- **stern**: Multi-pod log tailing
- **k9s**: UI de terminal para Kubernetes
- **kubectl-tree**: Ver jerarquía de recursos
- **kubectx/kubens**: Cambiar contextos y namespaces

## 📚 Recursos

- [Troubleshooting Applications](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application/)
- [Troubleshooting Clusters](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/)
- [Debug Running Pods](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-running-pod/)

## ✅ Checklist de Troubleshooting

- [ ] Verificar estado del Pod
- [ ] Revisar logs
- [ ] Inspeccionar eventos
- [ ] Verificar recursos
- [ ] Probar conectividad de red
- [ ] Validar configuración
- [ ] Revisar permisos RBAC
- [ ] Verificar almacenamiento
