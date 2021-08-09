# Laboratorio Kubernetes
Para este laboratorio se necesitará lo siguiente:
- Docker Desktop for Windows/Mac
- Go
- Kind Quick Start

## Descargar e Instalar Docker
- Descargamos [Docker](https://www.docker.com/products/docker-desktop) e instalamos.

## Instalamos Go
El instalador se encuentra en la siguiente [ruta](https://golang.org/doc/install).

### Para Mac
Ejecutar el siguiente comando en una terminal:

~~~
export PATH=$PATH:/usr/local/go/bin
~~~

### Para Windows

~~~
set | find "GO"
GOPATH=C:\Users\Administrator\go
GOROOT=C:\Go\
~~~
Validamos
~~~
go version
~~~
Output
~~~
go version go1.16.6
~~~
>La versión varía.

## Instalamos Kind Quick start
### Para Mac
En una terminal

~~~
brew install kind
~~~
>En caso no tenga instalado *brew*, revisar la [web oficial](https://brew.sh/index_es)

### Para Windows
En una terminal (PowerShell), busque una ruta donde quiera descargar el archivo (por ejemplo: D:\prueba) y ejecute el siguiente comando:

~~~
curl.exe -Lo kind-windows-amd64.exe https://kind.sigs.k8s.io/dl/v0.11.1/kind-windows-amd64
~~~

Luego modificar las variables de entorno en Inicio>Variables de Entorno y agregar el siguiente PATH:

~~~
D:\prueba\kind.exe
~~~

### Para Mac y Windows
Ejecutar el siguiente comando para validar lo instalado:
~~~
kind create cluster --config config_cluster.yaml
~~~
Output
~~~
Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.21.1) 🖼 
 ✓ Ensuring node image (kindest/node:v1.21.1) 🖼 
 ✓ Preparing nodes 📦 
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾
 ✓ Installing StorageClass 💾 
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Thanks for using kind! 😊
~~~
Validamos
~~~
mariocb@localhost Lab-K8S % kubectl get nodes
NAME                 STATUS   ROLES                  AGE     VERSION
kind-control-plane   Ready    control-plane,master   2m26s   v1.21.1
kind-worker          Ready    <none>                 2m26s   v1.21.1
kind-worker2         Ready    <none>                 2m26s   v1.21.1
~~~