# Cluster-setup/AWS Infrastructure and Kubernetes Cluster

```sh
# On all nodes
chmod +x cluster-setup.sh
./cluster-setup.sh
```

```sh
# On all nodes
chmod +x kubernetes-setup.sh
./kubernetes-setup.sh
```

```sh
# On master node
sudo kubeadm init

# if not working
systemctl stop unattended-upgrades
dpkg --configure -a
apt update
# do init again
```

```sh
# On master node
# Create the directory for kubeconfig file
mkdir -p $HOME/.kube

# Copy the admin.conf file to the kubeconfig directory
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

# Change ownership of the kubeconfig file to the current user
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

```sh
# On master node
# If you need to generate a new token use the below command (Optional Not required , if you have the above token generated)
sudo kubeadm token create --print-join-command
```

```sh
# On worker nodes
# Use the join command generated from the master node to join the worker nodes to the cluster
# Example:
sudo kubeadm join <master-node-ip>:6443 --token <token> --discovery
```

```sh
# On the control plane node, install Calico Networking:
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

# Check status of the control plane node:
kubectl get nodes

## Come back to Master node and executhe below commands (` Only on Master Node `)
```bash

# Verify the cluster status by executing kubectl command on the master node
kubectl get nodes
```

```sh
root@ip-172-31-0-49:/home/ubuntu/Cluster-setup# kubectl create ns dev
namespace/dev created
root@ip-172-31-0-49:/home/ubuntu/Cluster-setup# kubectl create ns prod
namespace/prod created
```
