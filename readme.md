# QANP CSI Driver for Kubernetes
This is official [Container Storage Interface](https://github.com/container-storage-interface) driver for QNAP NAS.

## Software Prerequisites
### CSI Driver version and Compatibility
| Driver Version  | Supported k8s version   | Supported QNAP NAS version |
| ----------------| ------------------------|----------------------------|
| v0.0.0-beta     |     1.14 to 1.23        | QuTS 5.0.0 or later        |

### Supported host operating systems
- Debian 8 or later
- Ubuntu 16.04 or later
- CentOS 7.0 or later
- RHEL 7.0 or later
- CoreOS 1353.8.0 or later

## Supported feature

# Deploy
## Before starting
### Additional install item in k8s environment
Master and worker node should install: 
Run `apt install open-iscsi`

### Qualify your Kubernetes cluster
1. **Minikube is not supported**
2. Make sure “kubectl” works well
   - Run `kubectl get pods`
   - Run `kubectl version`
3. Make sure you are Kubernetes cluster administrator
   - Run `kubectl auth can-i '*' '*' --all-namespaces`
   - The result should be yes
4. Can you launch a pod that uses an image from Docker Hub and can reach your storage system over the pod network?
   - Run `kubectl run -i --ttyping --image=busybox --restart=Never --rm --\ping <management IP>`
   - Example `kubectl run -i --tty ping --image=busybox --restart=Never --rm -- \ping 10.64.118.157`

## Start install QNAP CSI Plugin
1. Clone the git repository. `gh repo clone qnap-dev/QNAP-CSI-PlugIn`
2. Enter the directory. `cd QNAP-CSI-PlugIn`
3. Install helm (for Ubuntu)
   - curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
   - sudo apt-get install apt-transport-https --yes
   - echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
   - sudo apt-get update
   - sudo apt-get install helm
4. Install CSI Plugin
Run `helm install qnap-trident ./qnap-trident -n trident --create-namespace`

