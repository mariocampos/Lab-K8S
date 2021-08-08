## Luego de clonar el repositorio ingresamos a la carpeta
~~~
cd Ejercicios
~~~
## Creación de Namespace
1. Revisamos el archivo de Namespace clonado:
~~~
vim 000_namespace.yaml
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

~~~
5. Validamos
~~~
kubectl get ns
~~~
6. Output
~~~

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
kubectl create deployment apache --image=httpd --port=8080
deployment.apps/apache created
~~~
3. Validamos lo creado
~~~
kubectl get all
~~~
4. Output
~~~

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
apiVersion: v1
kind: Deployment
metadata:
  name: hello
spec:
  replicas: 3
  template:
    metadata:
      labels:
        role: hello
    spec:
      containers:
      - name: hello
        image: gcr.io/google-samples/hello-app:1.0
        ports:
        - containerPort: 8080
~~~
4. Ejecutamos el siguiente comando:
~~~
kubectl apply -f 02_deployment_v1.yaml
~~~
5. Output
~~~
de
~~~