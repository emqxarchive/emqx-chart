# 简介
本项目用于在 kubernetes 或 k3s 上部署 emqx broke (emqx edge) + emqx-control-center + prometheus 环境

# 如何使用

## 编译 emqx-control-center docker images
+ 在任意一台worker节点上执行 `git clone -b zhanght https://github.com/emqx/emqx-control-center.git`
+ 前端编译，在 emqx-control-center/frontend 目录环境下执行以下命令
    ```
    $ yarn build
    ```
+ 在 `emqx-control-center` 项目根目录环境下执行以下命令
    ```
    $ docker build -t ecc:latest .
    ```
## 启动kubernetes集群
以下两步任选其一执行
+ 编辑项目根目录下的 `value.yaml`文件，设置相关参数，执行 `helm install .` 启动集群
+ 执行 `helm install --set xxx .` 使用 `--set` 指定参数，启动集群 

## 配置 emqx-control-center
宿主机以nginx代理为例
+ 创建emqx appid 和 appsecret，详见[EMQX文档](https://developer.emqx.io/docs/emq/v3/en/commands.html)
+ 配置nginx，反向代理emqx-control-center
    + 使用kubectl get svc 获取emqx-control-center 的clusterIP
    + 配置nginx，将宿主机的8888端口和3000端口代理到emqx-control-center 的clusterIP
    + `nginx -s reload`
+ 浏览器打开 `http://hostIP:8888`，登录emqx-control-center的dashboard，默认用户名：admin 密码：public，打开 `系统管理-系统设置`, 填入 emqx 的 appid 和 appsecret。 

# Configuration
The following table lists the configurable parameters of the emqx chart and their default values.

| Parameter  | Description |
| ---        |  ---        |
| `globail.namespace`  | kubernetes namespace， Default:default |
| `globail.apiserver`  | **Required!** Kubernates API server address |
| `globail.apiserverToken`  |Token used for authentication by kube apiserver |
| `deployment.replicaCount` |  Default:2 |
| `deployment.image` | Default:latest  |
| `deployment.imagePullPolicy`  | Default:IfNotPresent  |
| `deployment.env.kubeAddressType`  | The address type is used to extract host from k8s service, Value: ip && dns,  Default:ip  |
| `deployment.nodeExporter`  | True or flase, Default: true |
| `service.type`  | Default:ClusterIP  |
| `service.mqttPort`  | Emqx cluster MQTT port, Default:1883  |
| `service.mqttsslPort` | Emqx cluster MQTT(SSL) port, Delfault:8883  |
| `service.mgmtPort`  | Emqx cluster mgmt API, Default:8080  |
| `service.websocketPort`  | Emqx cluster WebSocket/http port, Default:8083  |
| `service.wssPort`  | Emqx cluster WSS/HTTPS port, Default:8084  |
| `service.dashboardPort` | Emqx cluster dashboard port, Default: 18083 |
| `emqx-control-center.postgresPassword` | postgres password |
| `emqx-control-center.hostname` | Specify the host to be deployed by emqx-control-center. **The host must have the docker images of emqx-control-center** |
