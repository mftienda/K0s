## Instalación en un nodo.

El nodo controlador y el worker serán el mismo.

### 1.- Descarga de k0s

`curl -sSLf https://get.k0s.sh | sudo sh`

Con este comando, primero se descarga un script y a continuación se ejecuta.

Realmente lo que ha hecho es copiar k0s en /usr/local/bin/k0s y le ha dado permisos 755 a dicho archivo.

Podemos comprobar la versión instalada:

`k0s version`

### 2.- Procedemos a instalarlo el cluster.

sudo k0s install controller --single




### 3.- Iniciamos el clúster

sudo k0s start

### 4.Chequeamos el servicio

$ sudo k0s status

Version: v1.22.4+k0s.1
Process ID: 436
Role: controller
Workloads: true
Init System: linux-systemd
Access your cluster using kubectl

### 5.- k0s incluye kubectl

$ sudo k0s kubectl get nodes -o wide

NAME   STATUS   ROLES    AGE    VERSION
k0s    Ready    <none>   4m6s   v1.22.4-k0s1

### 6.-Comprobaciones
 
1.- Creamos un pod:

  `k0s kubectl run pod-nginx --image=nginx`
 
2.- Accedemos dentro del pod
  `k0s kubectl exec pod/pod-nginx -it -- /bin/bash`
  `echo " Soy Manolo" >/usr/share/nginx/html/index.html`

3.- Creamos una pasarela: port-forward
   `k0s kubectl port-forward pod/pod-nginx 8081:80`
 
4.- Con el navegador: IPPublica:8081
  
## Desinstalación de k0s
    
1.- Paramos el servicio:
`sudo k0s stop`

2.- Limpiamos la instalación:
`sudo k0s reset`

3.- Reiniciamos el sistema
  
