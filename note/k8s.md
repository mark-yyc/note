## 安装

1. 添加国内源：

   ```shell
   curl -s https://mirrors.aliyun.com/kubernetes/apt/doc/apt-key.gpg | sudo apt-key add -
   echo "deb https://mirrors.aliyun.com/kubernetes/apt/ kubernetes-xenial main" >>/etc/apt/sources.list.d/kubernetes.list
   ```

2. 下载Docker & Kubeadm & Kubelet & Kubernetes-cni

   ```shell
   apt-get install -y kubelet kubeadm kubectl docker.io
   //example
   apt-get install -y kubelet=1.20.0-00 kubeadm=1.20.0-00 kubectl=1.20.0-00 docker.io
   ```

   不指定版本就默认最新版

3. 关闭swap

   ```shell
   swapoff -a
   ```

4. 集群初始化（master node 创建）

   master node为单独一台主机，并且不能有其他pod运行

   官方镜像地址被墙，使用ali的源：

   ```shell
   kubeadm init --image-repository registry.aliyuncs.com/google_containers --kubernetes-version v1.20.0 --pod-network-cidr=192.168.0.0/16
   
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

   记录下token，用于节点的join
   
5. 安装calico网络插件
   参考:
   https://docs.projectcalico.org/getting-started/kubernetes/quickstart
   
6. 查看组件状态

   ```shell
   kubectl get cs
   ```

   是否出现unhealthy

   解决unhealthy问题：

   ```shell
   cd /etc/kubernetes/manifests
   vi kube-controller-manager.yaml
   vi kube-scheduler.yaml
   ```

   注释port=0

   systemctl restart kubelet

7. 其他节点加入集群：

   同样进行1，2，3操作

   ```shell
   kubeadm join 10.0.0.10:6443 --token ni5sot.otludm6qetlb18cs \
       --discovery-token-ca-cert-hash sha256:7062aabda5b278f21baf0f33591debcca36f88d6a4ed9ab6762a4b8c0219b149 
   ```

   token 和 hash 过期时间为1天

## 查看状态

1. 查看pod,service,deploment状态

   ```shell
   kubectl get namespace #查看所有的namespace
   kebectl get pod/svc/deployment
   ```

   -n  <namespace> 查看某个命名空间下的pod

   -o wide	查看详细信息

2. 执行yaml

   ```shell
   kubectl create -f pod.yaml #创建(只能单次)
   kubectl apply -f pod.yaml #更新
   ```

3. 扩展/缩减 副本

   ```shell
   kubectl scale <deployment> --replicas=<n>
   ```

4. 进入某个pod中的container
   ```shell
   kubectl exec -it mysql-5bb4fbf4f-glmm5  -- /bin/bash
   ```

5. 删除pods，deployment，service

   ```shell
   kubectl delete deployment/service/pod <name> -n <namespace>
   ```

6. 查看yaml文件:

   ```bash
   kubectl get pods/svc/deployment -o yaml
   ```

7. 直接编辑yaml

   ```bash
   kubectl edit pods/svc/deployment 
   ```

8. ```
   kubectl create secret generic elasticsearch-pw-elastic \
       -n elastic \
       --from-literal password=ZTBWxYGpyAsU7vOec6Ji
   ```

9. 
