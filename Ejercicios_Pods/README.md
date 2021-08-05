## Luego de clonar el repositorio ingresamos a la carpeta
~~~
cd Ejercicios
~~~
## Ejericio Pod
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
# Ejericio Deployment
1. 
