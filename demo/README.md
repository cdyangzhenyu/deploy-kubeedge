## 使用云端控制边缘端服务

### 启动用户应用的方式

选择边缘节点有两种方式，都是k8s原生支持的，一种是通过nodeName进行节点指定，一种是利用NodeSelector和node的label配合指定一系列节点。

#### 使用nodeName启动应用

具体配置见deployment.yaml

```
...
spec:
      nodeName: fb4ebb70-2783-42b8-b3ef-63e2fd6d242e
...
```

#### 使用NodeSelector启动应用

具体配置可参考deployment-armv7.yaml

```
...
  spec:
      nodeSelector:
        name: edge-node
...
```
之前在创建k8s node时，在node.json中定义过该label，如果要给不同的节点添加不同的label，只需通过label命令添加或者在node.json中添加即可。

### 启动应用

在云端执行：

```
kubectl apply -f deployment.yaml
```

默认是部署在了default命名空间，也可以在配置文件中指定其他命名空间

```
kubectl get pods

NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-64c448fd67-djxxw   1/1     Running   0          13m
```

可在边缘节点查看应用启动情况：

```
[root@fb4ebb70-2783-42b8-b3ef-63e2fd6d242e edge]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
6aaedf615b10        nginx:1.15.12       "nginx -g 'daemon of…"   16 minutes ago      Up 16 minutes                           k8s_nginx_nginx-deployment-64c448fd67-djxxw_default_096991e2-a7d6-4fe7-bd8e-79e93de5174a_0
```

这里的应用都是基于hostport启动的，也就是说上述服务直接暴露边缘节点的port 80

可以直接在浏览器访问：http://edge_ip

### 删除应用

在云端执行

```

kubectl delete -f deployment.yaml
```
