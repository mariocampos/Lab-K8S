## Luego de clonar el repositorio ingresamos a la carpeta
~~~
cd Ejercicios
~~~
## Creación de Namespace
1. Revisamos el archivo de Namespace clonado:
~~~
vim 00_namespace.yaml
~~~
2. Lo cual nos mostrará lo siguiente:
~~~
kind: Namespace
apiVersion: v1
metadata:
  name: test
~~~
>Donde al *namespace* le pondremos de nombre "test"
3. Guardamos y salimos del editor de texto, luego aplicamos con el siguiente comando:
~~~
kubectl apply -f 00_namespace.yaml
~~~
4. Luego de la ejecución anterior nos muestra el siguiente mensaje:
~~~
namespace/test created
~~~
5. Validamos
~~~
kubectl get ns
~~~
6. Output
~~~
NAME                 STATUS   AGE
default              Active   2d21h
kube-node-lease      Active   2d21h
kube-public          Active   2d21h
kube-system          Active   2d21h
local-path-storage   Active   2d21h
test                 Active   2m18s
~~~
## Creación de Pod
1. Revisamos el archivo creado:
~~~
cat pods_v1.yaml
~~~
2. Vemos lo siguiente:
~~~
apiVersion: v1
kind: Pod
metadata:
  name: prueba
spec:
  containers:
  - name: prueba
    image: nginx:alpine
~~~
3. Luego de guardar y salir del editor ejecutamos el siguiente comando:
~~~
kubectl apply -f pods_v1.yaml
~~~
4. Lo que nos mostrará la siguiente salida:
~~~
pod/prueba created
~~~
5. Validamos
~~~
kubectl get pods
~~~
6. Nos mostrará los siguiente:
~~~
NAME     READY   STATUS    RESTARTS   AGE
prueba   1/1     Running   0          2m11s
~~~
## Creación de Deployment
#### Deployment v1
1. Revisamos los Deployments creados.
~~~
kubectl get deployment
~~~
2. Ejecutamos la siguiente línea de comando para crear el Deployment
~~~
kubectl create deployment apache --image=httpd --port=8080 --namespace=test
deployment.apps/apache created
~~~
3. Validamos lo creado
~~~
kubectl get deployments -n test
~~~
4. Output
~~~
NAME     READY   UP-TO-DATE   AVAILABLE   AGE
apache   1/1     1            1           2m
~~~
5. A modo de prueba, escalaré de uno a dos pods. Esto para balancear la carga.
~~~
kubectl get pods -n test
~~~
6. Output
~~~
NAME                      READY   STATUS    RESTARTS   AGE
apache-748c6cf475-2422z   1/1     Running   0          116s
~~~
7. Ejecutamos lo siguiente para escalar los pods
~~~
kubectl -n test scale deployment apache --replicas 2
deployment.apps/apache scaled
~~~
>Aumentamos de 1 a 2 pods; en caso se quiera tenes más de 2 replicas aumentar
8. Validamos
~~~
kubectl -n test get pods
NAME                      READY   STATUS    RESTARTS   AGE
apache-748c6cf475-2422z   1/1     Running   0          36m
apache-748c6cf475-zkb65   1/1     Running   0          117s
~~~
#### Deployment v2
1. Luego de validar el deplyment anterior, lo eliminamos para realizar otra forma de crear un deplyment
~~~
kubectl delete deployment ...
deployment.apps deleted
~~~
2. Revisamos el archivo clonado:
~~~
vi 02_deployment_v1.yaml
~~~
3. Lo cual nos mostrará lo siguiente
~~~
apiVersion: apps/v1
kind: Deployment
metadata:
  name: prueba
spec:
  replicas: 3
  selector:
    matchLabels:
      app: prueba
  template:
    metadata:
      labels:
        app: prueba
    spec:
      containers:
      - name: prueba
        image: gcr.io/google-samples/hello-app:1.0
        ports:
        - containerPort: 8080
~~~
4. Ejecutamos el siguiente comando:
~~~
kubectl apply -f 02_deployment_v1.yaml -n test
~~~
5. Output
~~~
deployment.apps/hello created
~~~
6. Validamos
~~~
kubectl -n test get pods
NAME                      READY   STATUS    RESTARTS   AGE
prueba-6494bff58c-5kqv4   1/1     Running   0          14s
prueba-6494bff58c-dcdnq   1/1     Running   0          14s
prueba-6494bff58c-mp97h   1/1     Running   0          14s
~~~
## Creacion de DaemonSet
1. Revisamos el archivo que clonamos:
~~~
vi 03_daemontset.yaml
~~~
2. Output
~~~
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd-ds
spec:
  template:
    metadata:
      labels:
        name: fluentd
    spec:
      containers:
      - name: fluentd
        image: gcr.io/google-containers/fluentd-elasticsearch:1.20
  selector:
    matchLabels:
      name: fluentd
~~~
3. Ejecutamos lo siguiente:
~~~
kubectl apply -f 03_daemontset.yaml
daemonset.apps/fluentd-ds created
~~~
4. Validamos:
~~~
kubectl get pods -o wide
NAME               READY   STATUS    RESTARTS   AGE   IP           NODE           NOMINATED NODE   READINESS GATES
fluentd-ds-5672j   1/1     Running   0          77s   10.244.2.4   kind-worker2   <none>           <none>
fluentd-ds-kzmt8   1/1     Running   0          77s   10.244.1.4   kind-worker    <none>           <none>
~~~
>En la parte de *node* nos damos cuenta que la ejecución del DaemonSet a creado cada pod en cada nodo.
