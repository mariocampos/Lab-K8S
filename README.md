# Kubernetes
Kubernetes es una tecnología que permite orquestar contenedores (por ejemplo Docker), con ello utilizan los objetos de las API de Kubernetes.

Se especifíca el estado deseado del cluster mediante la interfaz de líneas de comando *kubectl*.

El Control Plane de Kubernetes consiste en un grupo de daemons que corre en tu clúster:

- El Master de Kubernetes es un conjunto de tres daemons que se ejecutan en un único nodo del clúster. Los daemons son los siguientes:

    * __*kube-apiserver*__ : El servidor API brinda servicios a las operaciones REST y proporciona la interfaz para el estado compartido del clúster a través del cual interactúan todos los demás componentes.
    * __*kube-controller-manager*__ : Este daemon es que se encarga de conectar con el API del Cloud Provider, como por ejemplo crear instancias, crear load balancer.
    * __*kube-scheduler*__ : 

- Los restantes nodos no master (workers) en tu clúster, ejecutan los siguientes nodos:

    * __*kubelet*__, el cual se comunica con el Master de Kubernetes.
    * __*kube-proxy*__ ,un proxy de red que implementa los servicios de red de Kubernetes en cada nodo.

## Objetos de Kubernetes
Los objetivos básicos:

* Pod: Es un set o grupo de uno o más contenedores con almacenamiento/red compartidos.
* Service: Son una forma de poder contactar aplicaciones, ya sea desde dentro del cluster o desde fuera
* Volume: Como en Docker, es un directorio o un disco que está atado a un Pod y viceversa. Esto puede servir para una base de datos ya que la información no se elimina en caso el Pod sea eliminado.
* Namespace: Es como una división lógica de tu cluster de Kubernetes que divide: el tráfico, la carga, etc.

Además los controladores son:

* ReplicaSet: Es un campo incluido en la cración de Pods que indica el número de replicas requerido. Cuando un ReplicaSet necesita crear nuevos Pods, utiliza su plantilla Pod.
* Deployment: Es un template para crear pods.
* StatefulSet: Al igual que en Deployment, getstiona Pods. La diferencia es que mantiene una identidad asociada a sus Pods.
* DaemonSet: Es un template para crear pods, pero a diferencia de Deployment, crea los pods en cada nodo(mayormente es creado para monitoreo).
* Job: Un Job crea uno o más Pods y se asegura de que un número específico de ellos termina de forma satisfactoria
