
# MicroK8s Cluster Join Guide

This guide provides step-by-step instructions to join a MicroK8s Kubernetes cluster on both **Linux** and **Windows** systems. 

---

## Prerequisites
- **MicroK8s Join Command**: Ensure you have the join command provided by the cluster admin.
  ```
  microk8s join 213.199.56.32:25000/979242010756a6f208fdf7ddde6686b3/9d89d6123053 --worker
  ```
- **Permissions**: You need `sudo` or `root` access on Linux. On Windows, you need **WSL 2** installed.

---

## Steps for Linux

1. **Install MicroK8s**  
   Run the following command to install MicroK8s:
   ```bash
   sudo snap install microk8s --classic
   ```

2. **Add Your User to MicroK8s Group** (Optional)  
   This allows you to use MicroK8s without needing `sudo` each time.
   ```bash
   sudo usermod -a -G microk8s $USER
   sudo chown -R $USER ~/.kube
   ```
   Log out and log back in for the group changes to take effect.

3. **Open Required Ports**  
   Make sure port `25000` is open in your firewall for communication with the cluster.
   ```bash
   sudo ufw allow 25000/tcp
   ```

4. **Join the MicroK8s Cluster**  
   Use the join command provided by your cluster administrator:
   ```bash
   microk8s join 213.199.56.32:25000/979242010756a6f208fdf7ddde6686b3/9d89d6123053 --worker
   ```

5. **Verify Connection**  
   Once joined, check that your node has successfully joined the cluster:
   ```bash
   microk8s kubectl get nodes
   ```

---

## Steps for Windows (Using WSL 2)

1. **Install WSL 2**  
   Open PowerShell as Administrator and run:
   ```powershell
   wsl --install
   ```

2. **Install Ubuntu in WSL 2**  
   Once WSL 2 is set up, install Ubuntu:
   ```powershell
   wsl --install -d Ubuntu
   ```

3. **Install MicroK8s in WSL**  
   Open the Ubuntu terminal in WSL and install MicroK8s:
   ```bash
   sudo snap install microk8s --classic
   ```

4. **Add Your User to MicroK8s Group** (Optional)  
   This allows easier access to MicroK8s commands without `sudo`:
   ```bash
   sudo usermod -a -G microk8s $USER
   sudo chown -R $USER ~/.kube
   ```
   Log out and back in for the changes to apply.

5. **Join the MicroK8s Cluster**  
   Run the join command provided by the cluster admin:
   ```bash
   microk8s join 213.199.56.32:25000/979242010756a6f208fdf7ddde6686b3/9d89d6123053 --worker
   ```

6. **Verify Connection**  
   After joining, list the nodes to confirm that your node is part of the cluster:
   ```bash
   microk8s kubectl get nodes
   ```

---

## Troubleshooting

- **Firewall Issues**: Ensure port `25000` is open on both your machine and the cluster master node.
- **Token Expiry**: If the join token expires, ask the cluster admin to generate a new one.
  
This guide should help you easily join a MicroK8s cluster on both Linux and Windows WSL 2 environments. Happy clustering!
