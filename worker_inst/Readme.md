<h1> To run and execute this query </h1>

# chmod +x worker_install.sh
# sudo ./worker_install.sh

overlay: This enables the OverlayFS file system driver. Kubernetes uses this so containers can share base image layers (like a base Ubuntu image) without duplicating files on your disk.

br_netfilter: This forces network traffic that moves across a network bridge (the virtual switch connecting your containers) to pass through the host operating system's firewall rules (iptables).

net.bridge.bridge-nf-call-iptables = 1 and ip6tables = 1: These lines tell the system to use standard Linux firewall rules (iptables) to filter and route traffic moving between containers. Without this, your Kubernetes Network Plugin (like Calico or Flannel) cannot enforce security policies or isolate Pods from each other.

net.ipv4.ip_forward = 1: This turns your worker server into a router. It allows the server to forward network traffic arriving on one network interface (like your physical network card) out through another network interface (like the virtual network inside a container). Without this, containers cannot talk to the internet or to other machines.

# cat <<EOF | sudo tee .. :
 This writes these configuration lines to permanent files on your hard drive so the settings do not disappear when you reboot the server.

# sudo modprobe ...: 
This activates the modules immediately right now so you do not have to restart.

# sudo sysctl --system: 
This reloads the system configuration to apply your changes instantly without a reboot.



