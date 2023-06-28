# kubernetes-efk

Elasticsearch-Fluentbit-Kibana EFK Kubernetes manifests

### Yêu cầu:

- Đã cài đặt cụm Kubernetes trên local hoặc trên máy ảo
- Đã cài đặt kubectl để tương tác với cụm Kubernetes

### Hướng dẫn khởi tạo cụm kubernetes với minikube:

#### Khởi tạo cụm K8s phiên bản 1.21.5 có 2 node (1 master + 1 worker) bằng minikube

```bash
minikube start --kubernetes-version=1.21.5 --driver=docker --nodes=2 --cpus=2 --memory=2048 --cni=calico --container-runtime=containerd -p star
```

#### Kiểm tra cụm đã lên

```bash
minikube profile list
minikube status -p star
kubectl get no -o wide
```

#### Cách ssh vào node

```bash
minikube profile list
minikube ssh -p star -n <node name>
```



### Các bước cài đặt:

1. Tạo namespace

   ```bash
   kubectl apply -f create_ns.yaml
   ```
2. Khởi tạo cụm Elasticsearch - single node

   ```bash
   kubectl apply -f elasticsearch/.
   ```
3. Khởi tạo Fluentbit thu thập log Kubernetes trên tất cả các node

   ```bash
   kubectl apply -f fluentbit/.
   ```
4. Cài đặt Kibana

   ```
   kubectl apply -f kibana/.
   ```
