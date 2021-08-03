# Kubernetes
Kubernetes es una tecnología que permite orquestar contenedores (por ejemplo Docker), con ello utilizan los objetos de las API de Kubernetes.

Se especifíca el estado deseado del cluster mediante la interfaz de líneas de comando *kubectl*.

El Control Plane de Kubernetes consiste en un grupo de daemons que corre en tu clúster:

- El Master de Kubernetes es un conjunto de tres daemons que se ejecutan en un único nodo del clúster. Los daemons son los siguientes:

    * __*kube-apiserver*__ : 
    * __*kube-controller-manager*__ : Este daemon es que se encarga de conectar con el API del Cloud Provider, como por ejemplo crear instancias, crear load balancer.
    * __*kube-scheduler*__ : 

- Los restantes nodos no master (workers) en tu clúster, ejecutan los siguientes nodos:

    * __*kubelet*__, el cual se comunica con el Master de Kubernetes.
    * __*kube-proxy*__ ,un proxy de red que implementa los servicios de red de Kubernetes en cada nodo.

## Objetos de Kubernetes
Los objetivos básicos:

* Pod: Es un set o grupo de uno o más contenedores con almacenamiento/red compartidos.
* Service
* Volume
* Namespace

Además los controladores son:

* ReplicaSet
* Deployment: Es un template para crear pods
* StatefulSet
* DaemonSet
* Job
