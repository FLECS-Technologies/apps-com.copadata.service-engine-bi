# zenon Service Engine Helm Chart

This is a Helm chart for deploying the zenon Service Engine on Kubernetes.

The used helm chart along with it's values can be found in the root folder and in /templates
In the examples below it is installed with the release name "service-engine"

## Preparation

Create a new kubernetes namespace (choose any name for the namespace "service-engine-ns")
```
kubectl create ns service-engine-ns
```

## Set Variables

Edit the variables for the helm chart (values.yaml) Especially the following ones:
- licensing.*.server  <- IP or Name of Licensing Server
- licensing.*.serial  <- Serial of License to use (license mist be activated on license server)

see values.yaml for more info

## Install

Install the helm chart (choose any name for the release name "service-engine" and namespace "service-engine-ns")
```
helm install service-engine . -n service-engine-ns
```

Wait a  until the pvc has been finished provisioning.
You can watch the statuses with the following command:
```
kubectl get pvc -n service-engine-ns -w
```

Copy your zenon project files to the persistent volume for the service-engine to start  
The location/access of the persistent volume is dependant on the used storage class and existing storage classes on your cluster.

See the Service Engine starting
You can monitor it's status with te following command:
```
kubectl get deployment -n service-engine-ns -w
```


## Uninstall

To unsinstall all ressources installed using this Helm chart, use the following command
```
helm uninstall service-engine
```

And don't forget to delete the kubernetes namespace if you don't need it anymore
```
kubectl delete ns service-engine-ns
```