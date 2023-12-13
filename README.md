# Ruso Platform - A GitOps Repository with FluxCD

## Requirements

- FLUXCD
- SOPS
- KUBECTL
- KUSTOMIZE
- GPG

## SOPS - Import Public Key

```bash
gpg --import ./clusters/{cluster-name}/.sops.pub.asc
```
