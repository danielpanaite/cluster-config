# Immich install instructions for v1.114.0

- Apply init for namespace and pvc creation

```bash
kubectl apply -f init.yaml
```

- Create postgres instance

```bash
kubectl apply -f postgres-secret.yaml
kubectl apply -f postgres.yaml
```

- Create redis instance

```bash
kubectl apply -f redis.yaml
```

- Apply immich helm chart with custom values

```bash
helm install --namespace immich immich immich/immich -f immich-values.yaml
```

- Modify created immich service with load balancer and label

```bash
labels:
    loadbalancer: cilium

type: LoadBalancer
loadbalancerIP: 10.0.0.112
```

Remove clusterIP lines from service

- Apply immich ingress

```bash
kubectl apply -f ingress.yaml
```