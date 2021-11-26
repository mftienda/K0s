## Instalación en un nodo.

El nodo controlador y el worker serán el mismo.

### 1.- Descarga de k0s

`curl -sSLf https://get.k0s.sh | sh`

Con este comando, primero se descarga un script y a continuación se ejecuta.

Realmente lo que ha hecho es copiar k0s en /usr/local/bin/k0s y le ha dado permisos 755 a dicho archivo.

Podemos comprobar la versión instalada:

`k0s version`

### 2.- Procedemos a instalarlo el cluster.

`k0s install controller --single`

<img src="https://github.com/mftienda/K0s/raw/main/img/cluster-1nodo.png" alt="cluster-1nodo" />


### 3.- Iniciamos el clúster

`k0s start`

### 4.Chequeamos el servicio

`k0s status`

Version: v1.22.4+k0s.1
Process ID: 436
Role: controller
Workloads: true
Init System: linux-systemd
Access your cluster using kubectl

### 5.- k0s incluye kubectl

`k0s kubectl get nodes -o wide`

NAME                  STATUS   ROLES    AGE     VERSION       INTERNAL-IP      EXTERNAL-IP   OS-IMAGE                         KERNEL-VERSION   CONTAINER-RUNTIME
debian200-k0s-1nodo   Ready    <none>   3m34s   v1.22.2+k0s   217.71.200.248   <none>        Debian GNU/Linux 11 (bullseye)   5.10.0-8-amd64   containerd://1.5.7

 
### 6.-Comprobaciones
 
1.- Creamos un pod:

  `k0s kubectl run pod-nginx --image=nginx`
 
 NAME            READY   STATUS    RESTARTS   AGE
pod/pod-nginx   1/1     Running   0          19s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   5m32s

 
2.- Accedemos dentro del pod
  `k0s kubectl exec pod/pod-nginx -it -- /bin/bash`
  `echo " Soy Manolo" >/usr/share/nginx/html/index.html`

3.- Creamos una pasarela: port-forward
   `k0s kubectl port-forward pod/pod-nginx 8081:80`
 
4.- Utilizando la herramienta tmux, previamente instalada, dividimos la pantalla en dos:
 
<img src="https://github.com/mftienda/K0s/raw/main/img/comprobacion-1.png" alt="comprobacion-1.png" />
 
  
## 7.- Si necesitamos desintalar k0s
    
1.- Paramos el servicio:
`k0s stop`

2.- Limpiamos la instalación:
`k0s reset`

3.- Reiniciamos el sistema
  `reboot`
