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
sudo apt install docker.io -y
```

- Docker post install

```bash
sudo usermod -aG docker $USER
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
sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --skip-phases=addon/kube-proxy
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
helm install cilium cilium/cilium --version 1.16.1 --namespace kube-system -f values.yaml
```

- Install Nginx Ingress

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.2/deploy/static/provider/baremetal/deploy.yaml
```

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
