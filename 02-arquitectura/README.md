# Arquitectura de Kubernetes

## 📋 Contenido

### 1. Control Plane Components

#### API Server (kube-apiserver)
- Punto de entrada para todas las operaciones REST
- Valida y procesa solicitudes
- Actualiza objetos en etcd

#### etcd
- Almacén de datos clave-valor distribuido
- Almacena el estado del cluster
- Backup y recuperación

#### Scheduler (kube-scheduler)
- Asigna Pods a Nodes
- Considera recursos, constraints y políticas
- Algoritmos de scheduling

#### Controller Manager (kube-controller-manager)
- Node Controller
- Replication Controller
- Endpoints Controller
- Service Account & Token Controllers

#### Cloud Controller Manager
- Interacción con proveedores cloud
- Node, Route, Service Controllers

### 2. Node Components

#### kubelet
- Agente que se ejecuta en cada node
- Asegura que los contenedores estén ejecutándose
- Reporta estado al API server

#### kube-proxy
- Mantiene reglas de red en los nodes
- Implementa Services
- Balancea carga

#### Container Runtime
- Docker, containerd, CRI-O
- Ejecuta contenedores

### 3. Add-ons

- DNS (CoreDNS)
- Web UI (Dashboard)
- Container Resource Monitoring
- Cluster-level Logging

## 🎯 Comandos Útiles

```bash
# Ver componentes del control plane
kubectl get pods -n kube-system

# Verificar salud del cluster
kubectl get componentstatuses

# Ver configuración de kubelet
kubectl get nodes -o wide

# Logs de componentes
kubectl logs -n kube-system <pod-name>
```

## 📚 Recursos

- [Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/)
- [Cluster Architecture](https://kubernetes.io/docs/concepts/architecture/)

## ✅ Checklist

- [ ] Entender componentes del Control Plane
- [ ] Conocer componentes de Node
- [ ] Comprender flujo de comunicación
- [ ] Entender rol de etcd
- [ ] Conocer add-ons comunes
