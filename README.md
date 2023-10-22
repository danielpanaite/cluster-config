# Kubernetes cluster configuration for v1.28

- Disable swap on all the nodes:

```bash
sudo swapoff -a
sudo nano /etc/fstab
```

- Add iptables rules

```bash
sudo modprobe overlay
sudo modprobe br_netfilter
sudo bash -c 'cat << EOF | sudo tee /etc/sysctl.d/k8s.conf
    net.bridge.bridge-nf-call-iptables  = 1
    net.ipv4.ip_forward                 = 1
    net.bridge.bridge-nf-call-ip6tables = 1
    EOF'
sudo sysctl --system
```

- Install container runtimes

```bash
sudo apt install containerd runc
```

- Prepare and install Docker

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
sudo apt update
sudo apt install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo   "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

- Docker post install

```bash
sudo usermod -aG docker $USER
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

- Install GOlang

```bash
wget https://go.dev/dl/go1.21.3.linux-amd64.tar.gz
sudo  tar -C /usr/local -xzf go1.21.3.linux-amd64.tar.gz
```

add GO to path: paste line at the end of .profile

```bash
export PATH=$PATH:/usr/local/go/bin
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

- Install Kubernetes

```bash
sudo apt update
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt update
sudo apt install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

- Init cluster with kubeadm, cri-dockerd runtime and calico CNI

Pod cidr 192.168 specified for calico to work
```bash
sudo kubeadm init --kubernetes-version=1.28.3 --pod-network-cidr=192.168.0.0/16 --cri-socket=unix:///var/run/cri-dockerd.sock
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
```

- Install Calico CNI

```bash
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.26.3/manifests/tigera-operator.yaml
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.26.3/manifests/custom-resources.yaml
```

- Install MetalLB

Prepare:
```bash
kubectl get configmap kube-proxy -n kube-system -o yaml | \
sed -e "s/strictARP: false/strictARP: true/" | \
kubectl apply -f - -n kube-system
```

Install via manifest:
```bash
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.12/config/manifests/metallb-native.yaml
```

Apply ip pool manifests:
```bash
kubectl apply -f ipaddresspool.yaml
kubectl apply -f l2advertisement.yaml
```