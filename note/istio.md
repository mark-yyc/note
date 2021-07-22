### istio安装

```bash
curl -L https://istio.io/downloadIstio | sh -
cd istio-
export PATH=$PWD/bin:$PATH
istioctl install --set profile=demo -y
```

sidecar注入

```bash
kubectl label namespace default istio-injection=enabled #自动注入（容易报错）
```

取消注入：

```bash
kubectl label namespaces default istio-injection-
```

或手动注入:

```bash
kubectl apply -f <(istioctl kube-inject -f xxx.yaml)
```

查看注入istio-injection了的ns：

```bash
kubectl get namespace -L istio-injection
```

流量的流动过程：

istio自身定义的ingressGateway->我们自己定义的Gateway->virtualService->service

istio的ingressgateway的默认网络类型是loadbalancer，可以修改为nodeport

```bash
kubectl patch service istio-ingressgateway -n istio-system -p '{"spec":{"type":"NodePort"}}'
```

访问时就可以通过任意node的ip+nodeport进行访问