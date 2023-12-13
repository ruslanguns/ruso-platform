# Ruso Platform - A GitOps Repository with FluxCD

## Requirements

- FLUXCD
- SOPS
- KUBECTL
- KUSTOMIZE
- GPG

## How to use SOPS

More information https://fluxcd.io/flux/guides/mozilla-sops/

### SOPS - Import Public Key

```bash
gpg --import ./clusters/{cluster-name}/.sops.pub.asc
```

### SOPS - Configuration file

```yaml
cat <<EOF > ./clusters/{cluster-name}/.sops.yaml
creation_rules:
  - path_regex: .*.yaml
    encrypted_regex: ^(data|stringData)$
    pgp: ${KEY_FP}
EOF
```

> make sure to replace `${KEY_FP}` with the fingerprint of the public key and `{cluser-name}` with the name of the cluster

### SOPS - Encrypt secret

> Make sure you have a configuration file: `./clusters/{cluster-name}/.sops.yaml`

```bash
sops --config clusters/{cluster-name}/.sops.yaml  --encrypt --in-place /path/to/secret.yaml
```

> Make sure you have a proper written Secret Manifest before encrypting the file since based on the configuration file
> the encrypted fields should be `data` or `stringData`

### SOPS - Add decryption to Kustomization

```yam
  decryption:
    provider: sops
    secretRef:
      name: sops-gpg
```
