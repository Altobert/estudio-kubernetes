# Almacenamiento en Kubernetes

## 📋 Contenido

### 1. Volumes
- Almacenamiento efímero en Pods
- Tipos de volumes comunes:
  - emptyDir
  - hostPath
  - configMap
  - secret

### 2. Persistent Volumes (PV)
- Recurso de almacenamiento en el cluster
- Ciclo de vida independiente de Pods
- Provisioning: estático vs dinámico
- Access Modes:
  - ReadWriteOnce (RWO)
  - ReadOnlyMany (ROX)
  - ReadWriteMany (RWX)
- Reclaim Policies:
  - Retain
  - Delete
  - Recycle

### 3. Persistent Volume Claims (PVC)
- Solicitud de almacenamiento por usuario
- Binding con PV
- Storage requests y limits

### 4. Storage Classes
- Provisioning dinámico
- Diferentes tipos de almacenamiento
- Parámetros específicos del provisioner

### 5. Volume Snapshots
- Snapshots de volumes
- Restore desde snapshots

## 🎯 Comandos Útiles

```bash
# Persistent Volumes
kubectl get pv
kubectl describe pv <pv-name>

# Persistent Volume Claims
kubectl get pvc
kubectl describe pvc <pvc-name>

# Storage Classes
kubectl get storageclass
kubectl describe storageclass <sc-name>

# Ver uso de volumes en Pods
kubectl get pods -o custom-columns=NAME:.metadata.name,VOLUMES:.spec.volumes[*].name

# Verificar binding
kubectl get pv,pvc
```

## 📝 Ejemplos de YAML

```yaml
# PersistentVolume
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-example
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: standard
  hostPath:
    path: /mnt/data

# PersistentVolumeClaim
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-example
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
  storageClassName: standard

# Pod usando PVC
apiVersion: v1
kind: Pod
metadata:
  name: pod-with-pvc
spec:
  containers:
  - name: app
    image: nginx
    volumeMounts:
    - mountPath: /usr/share/nginx/html
      name: storage
  volumes:
  - name: storage
    persistentVolumeClaim:
      claimName: pvc-example
```

## 🔍 Conceptos Importantes

### Static vs Dynamic Provisioning

**Static**: Administrador crea PVs manualmente
**Dynamic**: PVs creados automáticamente usando StorageClass

### Binding
- PVC se vincula a PV con características coincidentes
- Binding es one-to-one
- Binding es exclusivo

### Expansion
- Algunos StorageClasses permiten expansión
- `allowVolumeExpansion: true` en StorageClass

## 📚 Recursos

- [Volumes](https://kubernetes.io/docs/concepts/storage/volumes/)
- [Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
- [Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)

## ✅ Checklist

- [ ] Entender tipos de Volumes
- [ ] Crear PV y PVC
- [ ] Trabajar con StorageClasses
- [ ] Configurar provisioning dinámico
- [ ] Entender Access Modes
- [ ] Gestionar Reclaim Policies
