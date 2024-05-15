---
sidebar_position: 3
---

# Installation Steps
This section will guide you through the installation of both Kronos-Core, the Kubernetes Operator, and Kronos-CLI, the command-line interface for Kronos.
# Kronos-Core: Operator
## Using Release Files

To install Kronos-Core, you need to apply the necessary Kubernetes manifests to your cluster.
```bash
kubectl apply -f https://github.com/KronosOrg/kronos-core/releases/download/v0.4.0/kronos-core-0.4.0.yaml
```
## Using Helm 
[Helm](https://helm.sh/) is a package manager for Kubernetes that simplifies the deployment and management of applications. To install the operator using a Helm chart, follow these steps:

- Add the Helm repository:
```bash
helm repo add kronos-core https://kronosorg.github.io/kronos-chart/
```

- Update the Helm repositories:
```bash
helm repo update
```

- Check the default values:
Before installing the operator, it's a good practice to check the default values of the Helm chart. You can do this by running:
```bash
helm show values kronos-core/kronos-core
```

- Modify the Helm values (optional):
If you need to customize the installation, create a values.yaml file and specify the values you want to override. For example:
```yaml 
# values_example.yaml
metrics:
  serviceMonitor:
    create: true
```

- Install the operator:
Use the following command to install the operator with your custom values:
```bash
helm install <release-name> kronos-core/kronos-core --create-namespace true --namespace <installation-namespace> --version 0.4.0 -f values.yaml
```
:::note 
**values to replace**
- \<release-name>: Replace this with the name you want to give to this installation. It's used to identify the release of the Helm chart in your Kubernetes cluster.
- \<installation-namespace>: Replace this with the namespace where you want to install the operator. If the namespace doesn't exist, it will be created.
- values.yaml: Replace this with the path to your custom values file, if you have any. This file contains the values that you want to override from the default Helm chart values.
example: 
```
helm install my-kronos-core kronos-core/kronos-core --create-namespace true --namespace kronos-system --version 0.3.2 -f custom_values.yaml
```
:::



- Verify the installation:
You can verify that the operator has been installed successfully by checking the deployed resources in your Kubernetes cluster:
```bash
kubectl get all -n <installation-namespace>
```

- Upgrading the operator:
If you need to upgrade the operator to a new version, you can use the helm upgrade command:
```bash
helm upgrade <release-name> kronos-core/kronos-core -f values.yaml
```

- Uninstalling the operator:
```bash
helm uninstall <release-name>
```











# Kronos-CLI

To install Kronos-CLI, you can download the binary for your operating system from the Kronos repository.
- Download the Kronos-CLI binary from the Kronos repository releases page:
```bash
curl -LO https://github.com/KronosOrg/kronos-cli/releases/download/v1.0.0/kronos-cli 
```
- Make the binary executable (Linux/macOS):
```bash
chmod +x kronos-cli
```
- Move the binary to a directory in your PATH (Linux/macOS):
```bash
mv kronos-cli /usr/local/bin/
```
- Verify the installation by running kronos-cli in your terminal:
```bash
kronos-cli version
```