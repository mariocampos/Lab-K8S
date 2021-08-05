# Ejericio 1
1. Creamos el primer archivo referente a la creación de un pod:
~~~
mkdir Ejercicios_Pods
~~~
2. Luego creamos el archivo con extensión .yaml o .yml:
~~~
touch pods_v1.yaml
~~~
3. Editamos el archivo creado
~~~
vim pods_v1.yaml
~~~
4. Ponemos lo siguiente:
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
5. Luego de guardar y salir del editor ejecutamos el siguiente comando:
~~~
kubectl apply -f pods_v1.yaml
~~~
6. Lo que nos mostrará la siguiente salida:
~~~
pod prueba created
~~~