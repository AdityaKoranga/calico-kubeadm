# calico-kubeadm

## Starting your kubeadm cluster with calico

make sure kubeadm is installed

Disable swap for the current session by issuing the following command:
```bash
sudo swapoff -a
```

initialise kubeadm cluster. for calico cidr to used is 192.168.0.0/16.
```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```

```bash
mkdir -p $HOME/.kube
```
```bash
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
```
after run this if it asks for overwriting then type 'y' and press enter.

```bash
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Install Calico using the kubectl create command and the tigera-operator.yaml available online.
```bash
kubectl create -f https://docs.projectcalico.org/manifests/tigera-operator.yaml
```
Use the wget command to download custom-resources.yaml:
```bash
wget https://docs.projectcalico.org/manifests/custom-resources.yaml
```

```bash
kubectl create -f custom-resources.yaml
```

now check the pods of `calico-system` namespace
```bash
kubectl get po -A
```

