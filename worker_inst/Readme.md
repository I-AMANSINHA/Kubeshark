<h1> To run and execute this query </h1>

#chmod +x worker_install.sh
#sudo ./worker_install.sh

overlay: This enables the OverlayFS file system driver. Kubernetes uses this so containers can share base image layers (like a base Ubuntu image) without duplicating files on your disk.

br_netfilter: This forces network traffic that moves across a network bridge (the virtual switch connecting your containers) to pass through the host operating system's firewall rules (iptables).
