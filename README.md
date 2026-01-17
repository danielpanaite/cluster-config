# K3s cluster configuration for v1.34 on Ubuntu LTS 24.04

## Preparation

```bash
sudo apt update
sudo apt upgrade
```

#### Disable all motds and update static one
```bash
sudo chmod -x /etc/update-motd.d/*
sudo vim /etc/motd
```

#### Install k3s with flags
```bash
curl -sfL https://get.k3s.io | sh -s - --disable=traefik --disable=servicelb --write-kubeconfig-mode=644
```

#### Install k9s and set theme
```bash
LATEST_K9S=$(curl -s https://api.github.com/repos/derailed/k9s/releases/latest | jq -r .tag_name)
wget https://github.com/derailed/k9s/releases/download/${LATEST_K9S}/k9s_linux_amd64.deb
sudo apt install ./k9s_linux_amd64.deb

mkdir -p "$HOME/.config/k9s/skins"
curl -L https://github.com/catppuccin/k9s/archive/main.tar.gz | tar xz -C "$HOME/.config/k9s/skins" --strip-components=2 k9s-main/dist/catppuccin-macchiato.yaml
yq -i '.k9s.ui.skin = "catppuccin-macchiato"' ~/.config/k9s/config.yaml -y
```

#### Install Goldilocks helm chart for pod scaling recommendations
```bash
helm repo add fairwinds-stable https://charts.fairwinds.com/stable
helm repo update
helm install goldilocks fairwinds-stable/goldilocks --namespace goldilocks --create-namespace -f goldilocks/values.yaml
```

#### Label ns to be monitored by goldilocks
```bash
kubectl label ns <NAMESPACE> goldilocks.fairwinds.com/enabled=true
```

#### Install Tailscale operator
```bash
helm repo add tailscale https://pkgs.tailscale.com/helmcharts
helm repo update
helm upgrade --install \
tailscale-operator tailscale/tailscale-operator \
--namespace=tailscale --create-namespace  \
--set-string oauth.clientId=<ID> \
--set-string oauth.clientSecret=<SECRET> --wait
```

## Useful commands:

#### Aliases:

```bash
alias k="kubectl"
alias po="kubectl get po -A"
alias svc="kubectl get svc -A"
alias dep="kubectl get deployment -A"
alias pvc="kubectl get pvc -A"
alias wide="kubectl get po -A -o wide"
```
