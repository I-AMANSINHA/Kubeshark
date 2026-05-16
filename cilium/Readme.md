<h1> minikube cluster prepared for installing cilium. </h1>
DOC : - https://docs.cilium.io/en/stable/gettingstarted/k8s-install-default/

# COMMANDS:
- minikube start --cni=cilium



CILIUM_CLI_VERSION=$(curl -s https://raw.githubusercontent.com/cilium/cilium-cli/main/stable.txt)
CLI_ARCH=amd64
if [ "$(uname -m)" = "aarch64" ]; then CLI_ARCH=arm64; fi
curl -L --fail --remote-name-all https://github.com/cilium/cilium-cli/releases/download/${CILIUM_CLI_VERSION}/cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum}
sha256sum --check cilium-linux-${CLI_ARCH}.tar.gz.sha256sum
sudo tar xzvfC cilium-linux-${CLI_ARCH}.tar.gz /usr/local/bin
rm cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum}

- cilium version
- cilium hubble enable --ui

-----------------------------------------------------------------------------------------------------------------------------------
Note :- if this not works then you can use below one,
# 1. Wipe the cluster clean
minikube delete

# 2. Boot Minikube with a blank network setting (Disables 'kindnet' and pauses configuration)
minikube start --network-plugin=cni --cni=false

# 3. Use your freshly installed CLI to deploy Cilium from scratch
cilium install

# 4. Enable the visual dashboard
cilium hubble enable --ui

# 5. now to start and monitor
cilium hubble ui

- using port 12000 (by default)

