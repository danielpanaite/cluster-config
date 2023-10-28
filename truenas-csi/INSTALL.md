# Democratic-csi for TrueNAS NFS installation

## Prepare node

Install cifs and nfs
```
sudo apt install -y cifs-utils nfs-common
```

## Prepare TrueNAS nfs service

Enable options:
- Enable NFSv4
- NFSv3 ownership model for NFSv4
- Allow non-root mount

## Install with Helm

```
helm upgrade --install --create-namespace --values freenas-nfs.yaml --namespace democratic-csi nfs democratic-csi/democratic-csi
```

```
kubectl label --overwrite namespace democratic-csi pod-security.kubernetes.io/enforce=privileged
```

## Test pvc provisioning

```
kubectl apply -f pvc-nfs-test.yaml
```