# Configuración de Aplicaciones

## 📋 Contenido

### 1. ConfigMaps
- Almacena configuración no confidencial
- Key-value pairs
- Inyección en Pods:
  - Variables de entorno
  - Command-line arguments
  - Archivos en volumes

### 2. Secrets
- Almacena información sensible
- Tipos de secrets:
  - Opaque (generic)
  - kubernetes.io/service-account-token
  - kubernetes.io/dockerconfigjson
  - kubernetes.io/tls
- Base64 encoding
- Buenas prácticas de seguridad

### 3. Environment Variables
- Definición directa
- Desde ConfigMaps
- Desde Secrets
- Desde metadatos (Downward API)

### 4. Resource Management
- Resource Requests
- Resource Limits
- QoS Classes:
  - Guaranteed
  - Burstable
  - BestEffort
- LimitRanges
- ResourceQuotas

### 5. Downward API
- Exponer información del Pod a contenedores
- Metadatos y recursos disponibles

## 🎯 Comandos Útiles

```bash
# ConfigMaps
kubectl create configmap my-config --from-literal=key1=value1 --from-literal=key2=value2
kubectl create configmap app-config --from-file=config.properties
kubectl get configmaps
kubectl describe configmap <name>

# Secrets
kubectl create secret generic my-secret --from-literal=password=mysecretpassword
kubectl create secret docker-registry regcred --docker-server=<server> --docker-username=<user> --docker-password=<pass>
kubectl get secrets
kubectl describe secret <name>

# Ver contenido de secret (decoded)
kubectl get secret <name> -o jsonpath='{.data.password}' | base64 --decode

# Resource Quotas
kubectl get resourcequota
kubectl describe resourcequota <name>

# LimitRanges
kubectl get limitrange
kubectl describe limitrange <name>
```

## 📝 Ejemplos de YAML

```yaml
# ConfigMap
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  database_url: "postgres://db:5432"
  log_level: "info"
  config.json: |
    {
      "key": "value"
    }

# Secret
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  username: YWRtaW4=  # base64 encoded
  password: cGFzc3dvcmQ=

# Pod usando ConfigMap y Secret
apiVersion: v1
kind: Pod
metadata:
  name: app-pod
spec:
  containers:
  - name: app
    image: myapp:1.0
    env:
    - name: DATABASE_URL
      valueFrom:
        configMapKeyRef:
          name: app-config
          key: database_url
    - name: DB_PASSWORD
      valueFrom:
        secretKeyRef:
          name: db-secret
          key: password
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
  volumes:
  - name: config-volume
    configMap:
      name: app-config

# ResourceQuota
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-quota
  namespace: default
spec:
  hard:
    requests.cpu: "10"
    requests.memory: 20Gi
    limits.cpu: "20"
    limits.memory: 40Gi
    pods: "10"
```

## 🔍 Buenas Prácticas

- No almacenar secrets en Git
- Usar herramientas de gestión de secrets (Vault, Sealed Secrets)
- Definir siempre resource requests y limits
- Usar ConfigMaps para configuración por entorno
- Versionar ConfigMaps para rollbacks

## 📚 Recursos

- [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
- [Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)
- [Resource Management](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

## ✅ Checklist

- [ ] Crear y usar ConfigMaps
- [ ] Gestionar Secrets
- [ ] Configurar variables de entorno
- [ ] Definir resource requests/limits
- [ ] Entender QoS classes
- [ ] Trabajar con ResourceQuotas
