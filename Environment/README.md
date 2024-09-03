---
description: Environment init and install develepment tools.
icon: bullseye-arrow
---

# Overview

This is a Makefile for environtment init and install development tools.

[![GitHub Actions](https://img.shields.io/github/actions/workflow/status/yakir3/gitbook/make-test.yml?label=make-test&logo=github&logoColor=white)](https://github.com/yakir3/gitbook/actions/workflows/make-test.yml)

## Make help

Help info `make help`.

### MacOS
```bash
make macos
```

### Ubuntu
```bash
make ubuntu
```

## Others

### iTerm2

```bash
# Install
brew install iterm2

# Import config
Appfiles/iterm2/iterm2Profile.json

# Import iterm2-color
Appfiles/iterm2/Solarized_Darcula.itermcolors
Appfiles/iterm2/HaX0R_GR33N.itermcolors
```

### k3s

```bash
# Kernel module
lsmod |grep -E "nf_conntrack|br_netfilter"

# Master
curl -sfL https://get.k3s.io | sh -
cat /var/lib/rancher/k3s/server/node-token  # join token
# Disable traefik
kubectl -n kube-system delete helmcharts.helm.cattle.io traefik
kubectl -n kube-system delete helmcharts.helm.cattle.io traefik-crd
kubectl -n kube-system delete pod --field-selector=status.phase==Succeeded 
# Modify /etc/systemd/system/k3s.service
ExecStart=/usr/local/bin/k3s \
    server \
    --disable traefik \
    --disable traefik-crd \
##restart k3s server
rm /var/lib/rancher/k3s/server/manifests/traefik.yaml
systemctl daemon-reload
systemctl restart k3s

# Worker
curl -sfL https://get.k3s.io | K3S_URL=https://k3s_server_ip:6443 K3S_TOKEN=k3s_server_token sh -

# Get kubectl and helm client
apt install bash-completion
curl -LO https://dl.k8s.io/release/v1.27.3/bin/linux/amd64/kubectl
wget https://get.helm.sh/helm-v3.11.0-linux-amd64.tar.gz
cat >> ~/.bashrc << "EOF"
complete -o default -F __start_kubectl k
source <(kubectl completion bash)
source <(helm completion bash)
EOF

# kubectl client config
mkdir ~/.kube
cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
kubectl get pod -A
helm list
```



>Reference:
> 1. [HomeBrew Official](https://brew.sh)
> 2. [中科大镜像](https://mirrors.ustc.edu.cn/help/brew.git.html)
> 3. [iterm2colors](https://iterm2colorschemes.com/)
> 4. [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh)
> 5. [Vim Awesome](https://vimawesome.com/)
