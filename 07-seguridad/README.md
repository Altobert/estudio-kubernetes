# Seguridad en Kubernetes

## 📋 Contenido

### 1. Authentication
- Usuarios y Service Accounts
- Certificados
- Tokens
- Authentication strategies

### 2. Authorization
- RBAC (Role-Based Access Control)
- Node authorization
- Webhook mode
- ABAC (Attribute-Based Access Control)

### 3. RBAC
#### Roles y ClusterRoles
- Definen permisos
- Scope: namespace vs cluster-wide

#### RoleBindings y ClusterRoleBindings
- Asignan roles a sujetos
- Sujetos: Users, Groups, ServiceAccounts

### 4. Service Accounts
- Identidad para Pods
- Automounteo de tokens
- Gestión de permisos

### 5. Security Contexts
- Pod Security Context
- Container Security Context
- Configuraciones:
  - runAsUser, runAsGroup
  - fsGroup
  - readOnlyRootFilesystem
  - capabilities
  - privileged
  - allowPrivilegeEscalation

### 6. Pod Security Standards
- Privileged
- Baseline
- Restricted

### 7. Network Policies
- Control de tráfico entre Pods
- Políticas de ingress y egress
- Default deny

### 8. Secrets Management
- Encryption at rest
- External secret stores
- Sealed Secrets

### 9. Image Security
- Image scanning
- Image signing
- Private registries
- ImagePullSecrets

## 🎯 Comandos Útiles

```bash
# Service Accounts
kubectl create serviceaccount my-sa
kubectl get serviceaccounts
kubectl describe serviceaccount <name>

# RBAC
kubectl get roles
kubectl get rolebindings
kubectl get clusterroles
kubectl get clusterrolebindings

# Verificar permisos
kubectl auth can-i create deployments
kubectl auth can-i create deployments --as=user@example.com
kubectl auth can-i list pods --as=system:serviceaccount:default:my-sa

# Describir RBAC
kubectl describe role <role-name>
kubectl describe rolebinding <binding-name>

# Security Context
kubectl explain pod.spec.securityContext
kubectl explain pod.spec.containers.securityContext

# Ver Security Context de un Pod
kubectl get pod <pod-name> -o yaml | grep -A 10 securityContext
```

## 📝 Ejemplos de YAML

```yaml
# ServiceAccount
apiVersion: v1
kind: ServiceAccount
metadata:
  name: my-service-account
  namespace: default

# Role
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: default
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]

# RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: ServiceAccount
  name: my-service-account
  namespace: default
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io

# ClusterRole (cluster-wide)
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: secret-reader
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "list"]

# Pod con Security Context
apiVersion: v1
kind: Pod
metadata:
  name: secure-pod
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 3000
    fsGroup: 2000
  serviceAccountName: my-service-account
  containers:
  - name: app
    image: nginx
    securityContext:
      allowPrivilegeEscalation: false
      readOnlyRootFilesystem: true
      runAsNonRoot: true
      capabilities:
        drop:
        - ALL
        add:
        - NET_BIND_SERVICE
```

## 🔍 Mejores Prácticas

### General
- Principio de mínimo privilegio
- Usar RBAC siempre
- No ejecutar contenedores como root
- Escanear imágenes regularmente

### RBAC
- Crear roles específicos, no usar cluster-admin
- Usar RoleBindings en lugar de ClusterRoleBindings cuando sea posible
- Auditar permisos regularmente

### Security Context
- Siempre definir securityContext
- readOnlyRootFilesystem cuando sea posible
- Drop capabilities no necesarias
- runAsNonRoot: true

### Secrets
- Encryption at rest habilitado
- No commitear secrets en Git
- Usar external secret managers
- Rotar secrets regularmente

### Network
- Implementar Network Policies
- Default deny como baseline
- Limitar tráfico egress

## 📚 Recursos

- [Security](https://kubernetes.io/docs/concepts/security/)
- [RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
- [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/)
- [Security Best Practices](https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/)

## ✅ Checklist

- [ ] Configurar RBAC
- [ ] Crear Service Accounts
- [ ] Implementar Security Contexts
- [ ] Aplicar Pod Security Standards
- [ ] Configurar Network Policies
- [ ] Gestionar Secrets de forma segura
- [ ] Verificar permisos con auth can-i
