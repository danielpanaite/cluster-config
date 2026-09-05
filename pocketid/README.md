## PocketID configuration for Tailscale

Edit coredns:
```bash
kubectl edit cm coredns -n kube-system
```

After this block:
```
data:
  Corefile: |
    .:53 {
        errors
        health
```

Add
```bash
rewrite name exact auth.hyrax-ghoul.ts.net pocketid-egress.auth.svc.cluster.local
```

and make sure it's before this block:
```
ready
    kubernetes cluster.local in-addr.arpa ip6.arpa {
        pods insecure
        fallthrough in-addr.arpa ip6.arpa
    }
```