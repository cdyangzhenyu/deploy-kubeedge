## kubeedge 1.0版本部署步骤[官方](https://github.com/kubeedge/kubeedge)

### [1.部署云端服务](./cloud/README.md)

### 2.添加新的边缘节点到云端

修改node.js中的边缘节点名称，与实际情况对应，本例中是fb4ebb70-2783-42b8-b3ef-63e2fd6d242e
创建节点，在云端执行：
```
kubectl apply -f node.json
```

检查节点状态
```
[root@cloud deploy-kubeedge]# kubectl get nodes
NAME                                   STATUS     ROLES    AGE   VERSION
cloud                                  Ready      master   41h   v1.15.2
fb4ebb70-2783-42b8-b3ef-63e2fd6d242e   NotReady   edge     13s   
```

此时是NotReady状态，部署好了边缘节点服务之后，会变为Ready状态

### [3.部署边缘节点服务](./edge/README.md)

