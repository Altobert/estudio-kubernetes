# Ejercicios Prácticos

## 📋 Contenido

Esta sección contiene ejercicios prácticos para prepararse para las certificaciones de Kubernetes.

### Niveles de Dificultad
- 🟢 Básico
- 🟡 Intermedio
- 🔴 Avanzado

## 🎯 Ejercicios por Tema

### 1. Pods y Workloads

#### Ejercicio 1.1 🟢 - Crear un Pod simple
**Tarea:**
- Crear un Pod con nombre `nginx-pod` usando imagen `nginx:latest`
- El Pod debe tener label `app=web`
- Verificar que el Pod esté corriendo

#### Ejercicio 1.2 🟡 - Multi-container Pod
**Tarea:**
- Crear un Pod con dos contenedores:
  - Contenedor principal: nginx
  - Sidecar: busybox que hace `sleep 3600`
- Ambos contenedores deben compartir un volume emptyDir en `/shared`

#### Ejercicio 1.3 🟡 - Deployment con Rolling Update
**Tarea:**
- Crear un Deployment con 3 réplicas de nginx:1.19
- Actualizar a nginx:1.20 con estrategia RollingUpdate
- Verificar el rollout
- Hacer rollback a la versión anterior

#### Ejercicio 1.4 🔴 - StatefulSet
**Tarea:**
- Crear un StatefulSet para una base de datos
- 3 réplicas con nombres estables
- Cada Pod debe tener su propio PVC
- Crear un Headless Service

### 2. Servicios y Networking

#### Ejercicio 2.1 🟢 - Exponer Deployment
**Tarea:**
- Crear un Deployment de nginx con 2 réplicas
- Exponer el Deployment con un Service tipo ClusterIP en puerto 80
- Verificar endpoints
- Probar conectividad desde otro Pod

#### Ejercicio 2.2 🟡 - NodePort Service
**Tarea:**
- Crear un Service tipo NodePort
- Verificar que sea accesible desde fuera del cluster

#### Ejercicio 2.3 🔴 - Ingress
**Tarea:**
- Crear dos Deployments diferentes (app1, app2)
- Exponer cada uno con un Service
- Configurar Ingress para routing basado en path:
  - `/app1` → Service de app1
  - `/app2` → Service de app2

#### Ejercicio 2.4 🔴 - Network Policy
**Tarea:**
- Crear dos Namespaces: `frontend` y `backend`
- Deployar Pods en cada namespace
- Crear NetworkPolicy que solo permita tráfico de frontend a backend
- Denegar todo otro tráfico

### 3. Almacenamiento

#### Ejercicio 3.1 🟢 - Volume emptyDir
**Tarea:**
- Crear Pod con volume emptyDir
- Montar en `/data`
- Escribir archivo y verificar persistencia dentro del Pod

#### Ejercicio 3.2 🟡 - PersistentVolume y PVC
**Tarea:**
- Crear un PersistentVolume de 5Gi
- Crear un PersistentVolumeClaim que solicite 2Gi
- Crear un Pod que use el PVC
- Verificar binding

#### Ejercicio 3.3 🔴 - Dynamic Provisioning
**Tarea:**
- Crear un StorageClass
- Crear PVC que use ese StorageClass
- Verificar que el PV se cree automáticamente
- Usar en un Deployment

### 4. Configuración

#### Ejercicio 4.1 🟢 - ConfigMap
**Tarea:**
- Crear ConfigMap con datos de configuración
- Crear Pod que consuma el ConfigMap como:
  - Variables de entorno
  - Archivo montado

#### Ejercicio 4.2 🟡 - Secrets
**Tarea:**
- Crear Secret con credenciales
- Crear Pod que use el Secret
- Verificar que esté disponible en el contenedor

#### Ejercicio 4.3 🟡 - Resource Limits
**Tarea:**
- Crear Deployment con resource requests y limits
- Requests: 100m CPU, 128Mi memory
- Limits: 200m CPU, 256Mi memory
- Crear ResourceQuota en el namespace

### 5. Seguridad

#### Ejercicio 5.1 🟡 - ServiceAccount y RBAC
**Tarea:**
- Crear ServiceAccount
- Crear Role que permita leer Pods
- Crear RoleBinding
- Verificar permisos con `kubectl auth can-i`

#### Ejercicio 5.2 🔴 - Security Context
**Tarea:**
- Crear Pod con Security Context:
  - runAsNonRoot: true
  - readOnlyRootFilesystem: true
  - Drop all capabilities
- Verificar que funcione correctamente

#### Ejercicio 5.3 🔴 - RBAC Complejo
**Tarea:**
- Crear ClusterRole que permita ver todos los Pods
- Crear Role en namespace específico que permita crear Deployments
- Crear RoleBindings apropiados
- Probar permisos

### 6. Troubleshooting

#### Ejercicio 6.1 🟡 - Debug Pod Failing
**Tarea:**
Se proporciona un manifest con errores. Encontrar y corregir:
- Imagen incorrecta
- ConfigMap faltante
- Resource limits muy bajos

#### Ejercicio 6.2 🔴 - Debug Service
**Tarea:**
Un Service no está funcionando. Debug y fix:
- Verificar selector labels
- Verificar endpoints
- Probar conectividad

#### Ejercicio 6.3 🔴 - Debug PVC
**Tarea:**
Un PVC está en estado Pending. Investigar y resolver:
- StorageClass issues
- Capacity problems
- Access mode mismatch

## 🏋️ Simulacros de Examen

### Simulacro CKA
**Duración: 2 horas**

1. Configurar cluster (ETCD backup, upgrade)
2. Crear y gestionar workloads
3. Troubleshooting de aplicaciones
4. Configurar networking
5. Gestionar almacenamiento
6. RBAC y seguridad

### Simulacro CKAD
**Duración: 2 horas**

1. Pods y Deployments
2. ConfigMaps y Secrets
3. Multi-container Pods
4. Services y Networking
5. Persistent Volumes
6. Observability (logs, monitoring)

### Simulacro CKS
**Duración: 2 horas**

1. Cluster setup y hardening
2. System hardening
3. Minimize microservice vulnerabilities
4. Supply chain security
5. Monitoring, logging y runtime security

## 📝 Tips para el Examen

1. **Practica kubectl**
   - Usa alias: `alias k=kubectl`
   - Aprende flags comunes: `-o yaml`, `--dry-run=client`
   - Usa autocompletion

2. **Manejo de tiempo**
   - No te quedes atascado en un problema
   - Marca las difíciles y vuelve después
   - Lee bien las preguntas

3. **Uso de documentación**
   - Puedes usar kubernetes.io
   - Ten bookmarks preparados
   - Practica buscar rápido

4. **Imperative vs Declarative**
   - Usa imperative commands para rapidez
   - Genera YAML con `--dry-run=client -o yaml`
   - Edita y aplica

5. **Verificación**
   - Siempre verifica tu trabajo
   - `kubectl get`, `kubectl describe`
   - Prueba que funcione

## 📚 Recursos para Práctica

- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Killer.sh](https://killer.sh/) - Simulador oficial
- [KodeKloud](https://kodekloud.com/) - Labs interactivos
- [Play with Kubernetes](https://labs.play-with-k8s.com/)

## ✅ Checklist de Práctica

- [ ] Completar ejercicios básicos
- [ ] Completar ejercicios intermedios
- [ ] Completar ejercicios avanzados
- [ ] Hacer simulacros de examen
- [ ] Practicar troubleshooting
- [ ] Dominar kubectl commands
- [ ] Practicar con tiempo limitado
