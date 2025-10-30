# Servicios y Networking

## 📋 Contenido

### 1. Services
Abstracción para exponer aplicaciones

#### ClusterIP (default)
- Expone servicio internamente
- Solo accesible dentro del cluster

#### NodePort
- Expone servicio en puerto de cada Node
- Rango: 30000-32767

#### LoadBalancer
- Expone servicio externamente
- Usa load balancer del cloud provider

#### ExternalName
- Mapea servicio a un DNS externo

### 2. Ingress
- Gestiona acceso HTTP/HTTPS desde exterior
- Routing basado en host/path
- TLS/SSL termination
- Ingress Controllers (nginx, traefik, etc.)

### 3. Network Policies
- Controla tráfico entre Pods
- Reglas de ingress y egress
- Selección por labels
- Namespace isolation

### 4. DNS en Kubernetes
- CoreDNS
- Service discovery
- Resolución de nombres

### 5. Networking Concepts
- CNI (Container Network Interface)
- Pod networking
- Service networking
- Cluster networking

## 🎯 Comandos Útiles

```bash
# Services
kubectl expose deployment nginx --port=80 --type=ClusterIP
kubectl get services
kubectl describe service <service-name>

# Endpoints
kubectl get endpoints

# Ingress
kubectl get ingress
kubectl describe ingress <ingress-name>

# Network Policies
kubectl get networkpolicies
kubectl describe networkpolicy <policy-name>

# DNS
kubectl run -it --rm debug --image=busybox --restart=Never -- nslookup <service-name>

# Port forwarding (para testing)
kubectl port-forward service/<service-name> 8080:80
```

## 📝 Tipos de Service

```yaml
# ClusterIP
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: ClusterIP
  selector:
    app: MyApp
  ports:
    - port: 80
      targetPort: 8080

# NodePort
spec:
  type: NodePort
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30007

# LoadBalancer
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 8080
```

## 📚 Recursos

- [Services](https://kubernetes.io/docs/concepts/services-networking/service/)
- [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)
- [Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

## ✅ Checklist

- [ ] Crear diferentes tipos de Services
- [ ] Configurar Ingress
- [ ] Implementar Network Policies
- [ ] Entender DNS en Kubernetes
- [ ] Debugging de networking
