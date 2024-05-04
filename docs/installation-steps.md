---
sidebar_position: 3
---

# Installation Steps
This section will guide you through the installation of both Kronos-Core, the Kubernetes Operator, and Kronos-CLI, the command-line interface for Kronos.
# Kronos-Core: Operator
To install Kronos-Core, you need to apply the necessary Kubernetes manifests to your cluster.
```bash
kubectl apply -f https://github.com/KronosOrg/kronos-core/releases/download/v0.2.0/kronos.yaml
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