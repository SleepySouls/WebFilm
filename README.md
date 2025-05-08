1. Tạo EKS Cluster
2. Cài Ingress Nginx Controller 2 command:
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx \
  --create-namespace \
  --set controller.service.type=LoadBalancer \
  --set controller.replicaCount=1 \
  --set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \
  --set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
  --set controller.nodeSelector."kubernetes\.io/os"=linux
3. Build dockerfile với command docker build -t <image-name> .
4. Trong file values.yaml:
image:
  repository: <tên của image>
  tag: latest
  pullPolicy: IfNotPresent
5. Phần host ở ingress sửa lại theo domain, deploy trên EKS thì khi add dns của domain, chọn CNAME, lấy CNAME ở LoadBalancer của EKS
5. Deploy bằng helm chart với command helm instal <chart-name> <chart-repo>