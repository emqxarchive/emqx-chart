# Introduction
This chart bootstraps an emqx deployment on a Kubernetes cluster using the Helm package manager. This is experimental. It should not be used in a production environment

# Prerequisites
+ Kubernetes 1.6+

# Installing the Chart
To install the chart with the release name `my-emqx`:
```
$ git clone https://github.com/emqx/emqx-chart.git
$ cd emqx-chart
$ helm install --name my-emqx .
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
| `apiserver`  | Kubernates API server address |
| `namespace`  | kubernetes namespace， Default:default |
| `deployment.replicaCount` |  Default:3. It is recommended to have odd number of nodes in a cluster, otherwise the emqx cluster cannot be automatically healed in case of net-split.|
| `deployment.image` | Default:emqx/emqx:latest  |
| `deployment.imagePullPolicy`  | Default:IfNotPresent  |
| `deployment.nodeSelector` | Assigning emqx pods to nodes |
| `persistence.enabled` | Enable EMQX persistence using PVC |
| `persistence.accessMode` | PVC Access Mode for EMQX volume |
| `persistence.size` | PVC Storage Request for EMQX volume |
| `resources` | CPU/Memory resource requests/limits |
| `service.mqttPort`  | Emqx cluster MQTT port, Default:1883  |
| `service.mqttsslPort` | Emqx cluster MQTT(SSL) port, Delfault:8883  |
| `service.mgmtPort`  | Emqx cluster mgmt API, Default:8080  |
| `service.websocketPort`  | Emqx cluster WebSocket/http port, Default:8083  |
| `service.wssPort`  | Emqx cluster WSS/HTTPS port, Default:8084  |
| `service.dashboardPort` | Emqx cluster dashboard port, Default: 18083 |
| `emqxConfig` | Emqx configuration item, see the [documentation](https://github.com/emqx/emqx-docker#emq-x-configuration) |
| `emqxLicneseSecretName` | EMQX Enterprise Edition requires manual creation of a Secret containing the licensed content. Write the name of Secret to the value of "emqxLicneseSecretName" |
