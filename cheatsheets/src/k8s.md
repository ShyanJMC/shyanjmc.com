# Kubernetes

## Firewall

### - Master

> sudo firewall-cmd --permanent --add-port=6443/tcp

> sudo firewall-cmd --permanent --add-port=2379-2380/tcp

> sudo firewall-cmd --permanent --add-port=10250/tcp

> sudo firewall-cmd --permanent --add-port=10259/tcp

> sudo firewall-cmd --permanent --add-port=10257/tcp

> sudo firewall-cmd --reload

### - Worker

> sudo firewall-cmd --permanent --add-port=10250/tcp

> sudo firewall-cmd --permanent --add-port=30000-32767/tcp

> sudo firewall-cmd --reload

## SELinux

> sudo setenforce 1

> sed -i 's/SELINUX=permissive/SELINUX=enforcing/g' /etc/selinux/config

## CRI-O

> curl https://raw.githubusercontent.com/cri-o/packaging/main/get | sudo bash

> sudo systemctl enable --now crio

> sudo systemctl enable --now podman.socket

## Kube repo

- /etc/yum.repos.d/kubernetes.repo
```
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.29/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.29/rpm/repodata/repomd.xml.key
exclude=kubelet kubeadm kubectl cri-tools kubernetes-cni
```

> sudo dnf install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

## kube-controller-manager

Archivo; /etc/kubernetes/manifests/kube-controller-manager.yaml

Debe llevar los siguientes flags;

-  "--allocate-node-cidrs=true"
-  "--cluster-cidr=<your-pod-cidr>"

## Ubicaciones

- Kubeconfig

Todas las distribuciones

> ~/.kube/config

> kubectl --kubeconfig [path_location]

> $KUBECONFIG

Rancher Goverment (RKEv2)

> /etc/rancher/rke2/rke2.yaml

Kubernetes bare metal

> /etc/kubernetes/admin.conf

## Tags - Roles 

Posibles roles para los nodos;

- worker
- control-plane
- etcd
- master

Asignar un rol

> kubectl label node [node_name] node-role.kubernetes.io/[role]=[tag_any_name]

Borrar un rol

> kubectl label node [node_name] node-role.kubernetes.io/[role]-

## Persistent Volume (PV)

Sirve para que independientemente de la instancia de POD, se pueda usar el volumes
en cada despliegue, se definen mediante el StorageClass.

Si se maneja bien los espacios y los nombres, se puede usar un PV y su PVC para 
pods especificos.

A diferencia de los volumenes comunes, estos no varian dependiendo de la instancia, por eso
son "persistent".

**El PV no se usa en el master, si no que afecta a los worker**.

- Volumen persistente manual

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: [pv_name]
  labels:
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```

Luego se puede crear el PersistentVolumeClaim para que pueda usar un espacio determinado
según el PV que lo satisfaga

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: [pvc_name]
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```

Ejemplo de un POD con un PVC específico

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: task-pv-pod
spec:
  volumes:
    - name: task-pv-storage
      persistentVolumeClaim:
        claimName: task-pv-claim
  containers:
    - name: task-pv-container
      image: nginx
      ports:
        - containerPort: 80
          name: "http-server"
      volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: task-pv-storage
```

## Backups

- ETCD

Rancher Goverment (RKEv2)

> rke2 etcd-snapshot save --name pre-upgrade-snapshot

> systemctl stop rke2-server && rke2 server --cluster-reset --cluster-reset-restore-path=[PATH-TO-SNAPSHOT] && systemctl start rke2-server

## Comandos

> sudo KUBECONFIG=[path_absoluto] kubectl ....

### - Unir al cluster

Kubernetes bare metal

> kubeadm join --discovery-token [master_token] --discovery-token-ca-cert-hash sha256:[HASH] --control-plane [master_IP]:6443

### - Aplicar deployment

Apply sobre escribirá si ya existe el recurso

> kubectl apply -f [file_or_URLfile]

- "-l [key]=[value]" asignar tag
- "-k [ditectory]" aplica varios deployments a la vez

Mientras que "create" no sobre escribirá

> kubectl create -f [file_or_URLfile]

- "-l [key]=[value]" asignar tag
- "-k [ditectory]" aplica varios deployments a la vez

En ambos ("create" y "apply") los tipos que se soportan son;

1. clusterrole
2. clusterrolebinding
3. configmap
4. cronjob
5. deployment
6. ingress
7. job
8. namespace
9. poddisruptionbudget
10. priorityclass
11. quota
12. role
13. rolebinding
14. secret
15. secret docker-registry
16. secret generic
17. secret tls
18. service
19. service clusterip
20. service externalname
21. service loadbalancer
22. service nodeport
23. serviceaccount
24. token
25. pv
26. pvc

### - Editar deployment

Se usa el editor especificado en la variable de entorno KUBE_EDITOR ó EDITOR

> kubectl edit [type]/[resource_name]

- "-o json" edita usando el modo json
- "-o yaml" edita usando el modo yaml

### - Mostrar eventos

Para todo el clúster

> kubectl events --all-namespaces

Para un pod específico

> kubectl events --for pod/[pod_name] --watch

### - Customizar salida

> ... -o [yaml,json,wide,etc]

### - Obtener información

> kubectl get [info] -o yaml

1. nodes
2. deployments
3. pods
4. svc (services)
5. rc (replication controller)
6. pv (persistent volume)
7. pvc (persistent volume claim)

> kubectl cluster-info

- "--storage-driver-password [string]" contraseña para la base de datos
- "--storage-driver-host [ip]:[port]" ip y puerto para la base de datos
- "--storage-driver-db [name]" nombre de la base de datos
- "--storage-driver-table [name]" nombre de la tabla
- "--storage-driver-user [name]" nombre de usuario
- "-s [ip]:[port]" ip y puerto del servidor


### - Obtener una descripción

> kubectl describe [recurso] -o yaml

Recursos compatibles

1. nodes
2. deployments
3. pods
4. svc (services)
5. rc (replication controller)

### - Inspeccionar pod

> kubectl inspect pods/[podname]

### - Ver registros (logs)

> kubectl logs [pod_name]

- "--tail=X" las últimas X líneas
- "--since=Xh" las últimas X horas
- "-c [container_name]" de un contenedor específico de ese POD
- "--previous" contenedores previos fallidos
- "--all-containers" todos los contenedores de ese pod

### - Adjuntar a container

> kubectl attach [pod_name]

- "-c [container_name]" a un contenedor específico
- "... -i -t" interactive y TTY
- "rs/[pod_name]" primera réplica del pod

### - Ejecutar en un contenedor

> kubectl exec [pod_name] -c [container] -i -t -- [comand] [command_arguments]

### - Auditar autenticación

> kubectl auth

- "--storage-driver-password [string]" contraseña para la base de datos
- "--storage-driver-host [ip]:[port]" ip y puerto para la base de datos
- "--storage-driver-db [name]" nombre de la base de datos
- "--storage-driver-table [name]" nombre de la tabla
- "--storage-driver-user [name]" nombre de usuario
- "-s [ip]:[port]" ip y puerto del servidor

### - Setear auto escalado horizontal

> kubectl autoscale [type] [resource] --min=[X] --max=[Y] --cpu-percent=[Z]

Tipos;

1. deployments
2. pods
3. svc (services)
4. rc (replication controller)

### - Setear escalado manual

> kubectl scale --replicas=[X] [type]/[resource_name]

### - Aprobar una solicitud de firmar un certificado (CSR: Certificate Signing Request)

> kubectl certificate approve [CSR_name]

- "-f [file_or_URLFile]" si no está el nombre, se puede usar un archivo
- "-R" si se usó "-f" y son más de un archivo se puede especificar esto para que lea todo el directorio
- "--force"
- "-h"

### - Marcar nodo como inusable 

Esto hace que el scheduler del master no mande algo a ejecutar

> kubectl cordon [node]

También se lo puede marcar como "drain" para realizar tareas de mantenimiento

> kubectl dran [node]

### - Copiar desde/hacia el POD

El src ó dest puede ser la máquina local, el otro tiene que ser el POD.

El pod se especifica; [namespace]/[pod_name]:[absolute_path]

> kubectl cp [src] [dest]

### - Debug resource

> kubectl debug [type]/[resource_name] -it --image=[busybox,debian,etc]

- "-c [containers_pod]" especificamente para los tipos; pod

### - Borrar recursos

> kubectl delete [type-1],[type-n] [resource_name]

### - Ver diferencias entre configuraciones

La diferencia es entre el archivo de deployment original y la configuración actual del recurso

> kubectl diff -f [file]

### - Crear un servicio en un pod existente

> kubectl expose [type] [resource_name] --port=[host_port] --target-port=[container_port] --name=[service_name]

- "-f [archivo].yaml" también se puede usar un archivo en vez de especificar el tipo

### - Actualizar labels en un recurso

> kubectl label --overwrite [type] [resource_name] [label]=[value]

- "-f [archivo].yaml" también se puede usar un archivo en vez de especificar el tipo

### - Exponer puerto sin crear servicios

> kubectl port-forward [type]/[resoource_name] [host_port]:[container_port] --address [ip_where_allow_incoming]

### - Proxy HTTP para acceder a la API de Kubernetes

Se inicia un proxy entre el host donde ejecutamos y el clúster para poder consumir la API de Kubernetes

> kubectl proxy --port=[port_to_use] --address=[ip_master_node]

La URL luego tiene esta forma;

> http://localhost:8080/api/v1/proxy/namespaces/[namespace]/services/[service]

Se debe usar kubectl config para especificar usar ese proxy

> kubectl config set-context [name] --proxy=http://[proxy_ip]:[port]

> kubectl proxy -n default --url http://[proxy_ip]:[port]

### - Remplazar/actualizar POD

> kubectl replace -f [file].[yaml/json]

### - Rollback

Son soportados; deployments, daemonsts, statefulsets.

> kubectl rollout undo [type]/[resource_name]

> kubectl rollout status [type]/[resource_name]

> kubectl rollout restart [type]/[resource_name]

> kubectl rollout history

> kubectl rollout [pause/resume] [type]/[resource_name]

> kubectl rollout undo [type]/[resource_name]

Se puede incluir el argumento "--selector=app=[name]" en vez del tipo y nombre_recurso.

### - Crear POD

> kubectl run [name] --image=[image] --port=[container_port] --env=[environment_variable] --labels="[var]=[value],[var2]=[value2]" --restart=[Never/Always] -t -i

### - Ver consumo de recursos

> kubectl top [node/pod]/[resource_name]
