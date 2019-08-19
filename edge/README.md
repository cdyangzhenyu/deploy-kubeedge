## 边缘节点部署

### 修改配置文件conf/edge.yaml

websocket.url根据实际情况修改，主要修改的是云端的ip，websocket的端口，本例中是31000
修改所有的fb4ebb70-2783-42b8-b3ef-63e2fd6d242e内容为边缘节点实际的hostname，也需要和node.json中对应

### 从云端拷贝证书到边缘节点，具体证书如下：

cafile: /etc/kubeedge/ca/rootCA.crt
certfile: /etc/kubeedge/certs/edge.crt
keyfile: /etc/kubeedge/certs/edge.key


### 在边缘节点执行：
    ```shell
    # run mosquitto
    mosquitto -d -p 1883
    # or run emqx edge
    # emqx start
    
    # run edge_core
    # `conf/` should be in the same directory as the cloned KubeEdge repository
    # verify the configurations before running edge(edge_core)
    ./edge_core
    # or
    nohup ./edge_core > edge_core.log 2>&1 &
    ```
    **Note:** Please run edge using the users who have root permission.

#### 使用systemd管理服务

```shell
cp -r conf /etc/kubeedge/
cp x86_64/edge_core /etc/kubeedge/
cp edge.service /etc/systemd/system/
systemctl daemon-reload
systemctl restart edge
tailf /var/log/message
```
