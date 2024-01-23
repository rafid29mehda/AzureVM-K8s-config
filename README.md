# AzureVM-K8s-config

Setting up Kubernetes on an Azure VM involves several steps. Below is a simplified guide to help you get started. Please note that this is a basic overview, and you might need to refer to the official documentation for more detailed information. Also, keep in mind that the process may change, so it's essential to refer to the latest Azure and Kubernetes documentation.

### Step 1: Create an Azure Account
If you don't have an Azure account, sign up for one at [Azure Portal](https://portal.azure.com/).

### Step 2: Create a Virtual Machine (VM)
1. In the Azure Portal, navigate to "Virtual machines" and click on "Add" to create a new VM.
2. Follow the wizard to configure the VM settings, such as the operating system, size, and authentication.
3. Open necessary ports for Kubernetes. At least ports 80, 443, and 6443 should be open.

### Step 3: Install Docker
Connect to your VM, and install Docker:
```bash
sudo apt update
sudo apt install docker.io
```

### Step 4: Install Kubernetes Tools (kubeadm, kubelet, kubectl)
1. Add the Kubernetes repository:
   ```bash
   sudo apt-get update && sudo apt-get install -y apt-transport-https curl
   curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
   sudo apt-get update
   ```

2. Install Kubernetes tools:
   ```bash
   sudo apt-get install -y kubelet kubeadm kubectl
   ```

### Step 5: Initialize Kubernetes Cluster
Run the following commands to initialize the Kubernetes cluster:
```bash
sudo kubeadm init
```

### Step 6: Configure kubectl
Follow the instructions provided by kubeadm to set up kubectl:
```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### Step 7: Deploy a Pod Network (e.g., Calico)
Choose a pod network add-on and deploy it. For example, with Calico:
```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

### Step 8: Join Nodes (if applicable)
If you plan to have multiple nodes, use the provided join command displayed after initializing the master.

### Step 9: Verify Cluster Status
Check if the nodes are ready:
```bash
kubectl get nodes
```

### Step 10: Deploy Applications
Now, you can deploy your applications using `kubectl`.



**Note:** The commands and procedures may vary depending on the Azure and Kubernetes versions. Always refer to the official documentation for the most up-to-date information.
