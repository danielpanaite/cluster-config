# Kubernetes cluster configuration for v1.31 on Ubuntu LTS 24.04

- Disable swap on all the nodes:

```bash
sudo swapoff -a
sudo nano /etc/fstab
```

- Prepare and install Docker

```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl gpg -y
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

- Docker post install

```bash
sudo usermod -aG docker $USER
```

- Install Docker CRI

```bash
git clone https://github.com/Mirantis/cri-dockerd.git
sudo apt install make
cd cri-dockerd
make cri-dockerd
mkdir -p /usr/local/bin
sudo install -o root -g root -m 0755 cri-dockerd /usr/local/bin/cri-dockerd
sudo install packaging/systemd/* /etc/systemd/system
sudo sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service
sudo systemctl daemon-reload
sudo systemctl enable --now cri-docker.socket
```

Edit the sandbox pause container:
```bash
sudo nano /etc/systemd/system/cri-docker.service
```
Add --pod-infra-container-image=registry.k8s.io/pause:3.10 in the ExecStart line

Reload the systemd daemon:
```bash
sudo systemctl daemon-reload
```

Restart cri-dockerd service
```bash
sudo systemctl restart cri-docker

```

- Install GOlang

```bash
wget https://go.dev/dl/go1.23.0.linux-amd64.tar.gz
sudo  tar -C /usr/local -xzf go1.23.0.linux-amd64.tar.gz
```

add GO to path: paste line at the end of .profile

```bash
export PATH=$PATH:/usr/local/go/bin
```

- Install Kubernetes

```bash
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt update
sudo apt install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

- Init cluster with kubeadm

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --skip-phases=addon/kube-proxy --cri-socket=unix:///var/run/cri-dockerd.sock
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
```

- Install Cilium CLI

```bash
CILIUM_CLI_VERSION=$(curl -s https://raw.githubusercontent.com/cilium/cilium-cli/main/stable.txt)
CLI_ARCH=amd64
if [ "$(uname -m)" = "aarch64" ]; then CLI_ARCH=arm64; fi
curl -L --fail --remote-name-all https://github.com/cilium/cilium-cli/releases/download/${CILIUM_CLI_VERSION}/cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum}
sha256sum --check cilium-linux-${CLI_ARCH}.tar.gz.sha256sum
sudo tar xzvfC cilium-linux-${CLI_ARCH}.tar.gz /usr/local/bin
rm cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum}
```

- Install Cilium CNI

```bash
cilium install --version v1.16.1 --set kubeProxyReplacement=true --set k8sServiceHost=10.0.2.80 --set k8sServicePort=6443 --set l2announcements.enabled=true --set l2announcements.leaseDuration="3s" --set l2announcements.leaseRenewDeadline="1s" --set l2announcements.leaseRetryPeriod="500ms" --set externalIPs.enabled=true --set operator.replicas=1 --set ipam.operator.clusterPoolIPv4PodCIDRList=10.244.0.0/16
```

- Enable Hubble UI

```bash
cilium hubble enable --ui
```

- Install Nginx Ingress

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.2/deploy/static/provider/baremetal/deploy.yaml
```
Edit the service to type LoadBalancer and assign IP

## Useful k8s commands:

- #### Reclaim used PV:

```bash
kubectl patch pv pv-name -p '{"spec":{"claimRef": null}}'
```

- #### Useful bashrc aliases:

```bash
alias k="kubectl"
alias po="kubectl get po -A"
alias svc="kubectl get svc -A"
alias wide="kubectl get po -A -o wide"
```

- #### Sealed secrets commands:

```bash
kubeseal -f secret.yaml -w sealedsecret.yaml
kubectl create -f sealedsecret.yaml
```
To get the secret values:
```bash
kubectl get secret secret -o yaml
```

- #### DDNS crontab entry:

```bash
*/10 * * * * /home/sushi/ddns >/dev/null 2>&1
```

- #### Mount smb share:

```bash
mount -t cifs -o username=sushi //10.0.0.20/share /home/user/share
```
fstab:
```bash
//10.0.0.20/media /home/ cifs uid=1000,iocharset=utf8,file_mode=0776,dir_mode=0776,noperm 0 0
```

- #### Mount nfs share:

```bash
sudo mount -t nfs 10.0.0.20:/mnt/it-nas-6tb/volume /home/user/share
```
fstab:
```bash
10.0.0.20:/mnt/it-nas-6tb/k8s/volumes/ /home/  nfs defaults 0 0
```