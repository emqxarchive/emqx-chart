# Introduction
This chart bootstraps an emqx deployment on a Kubernetes cluster using the Helm package manager.

# Prerequisites
+ Kubernetes 1.6+

# Installing the Chart
To install the chart with the release name `my-emqx`:
```
$ git clone https://github.com/emqx/emqx-helm.git
$ cd emqx-helm
$ helm install --name my-emqx --set env.kubeApiserver=http://xx.xx.xx.xx:port .
```

# Uninstalling the Chart
To uninstall/delete the `my-emqx` deployment:
```
$ helm delete my-emqx
```

# Configuration
The following table lists the configurable parameters of the emqx chart and their default values.

| Parameter  | Description |
| ---        |  ---        |
| `replicaCount` |  Default:2 |
| `image.tag` | Default:latest  |
| `image.pullPolicy`  | Default:IfNotPresent  |
| `secret.apiserverToken` | Token used for authentication by kube apiserver |
| `env.kubeApiserver`  | **Required!** Kubernates API server address |
| `env.kubeNamespace`  | kubernetes namespace， Default:default |
| `env.kubeAddressType`  | The address type is used to extract host from k8s service, Value: ip && dns,  Default:ip  |
| `service.mqttPort`  | Emqx cluster MQTT port, Default:1883  |
| `service.mqttsslPort` | Emqx cluster MQTT(SSL) port, Delfault:8883  |
| `service.mgmtPort`  | Emqx cluster mgmt API, Default:8080  |
| `service.websocketPort`  | Emqx cluster WebSocket/http port, Default:8083  |
| `service.wssPort`  | Emqx cluster WSS/HTTPS port, Default:8084  |
| `service.dashboardPort` | Emqx cluster dashboard port, Default: 18083 |
