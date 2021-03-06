---
title: Selector-based policies
redirect_from: latest/reference/host-endpoints/selector
canonical_url: 'https://docs.projectcalico.org/v3.9/reference/host-endpoints/selector'
---


We recommend using selector-based security policy with
bare-metal workloads. This allows ordered policy to be applied to
endpoints that match particular label selectors.

For example, you could add a second policy for webserver access:

```
cat << EOF | dist/calicoctl create -f -
- apiVersion: projectcalico.org/v3
  kind: GlobalNetworkPolicy
  metadata:
    name: webserver
  spec:
    selector: "role==\"webserver\""
    order: 100
    ingress:
    - action: Allow
      protocol: TCP
      destination:
        ports: [80]
    egress:
    - action: Allow
EOF
```
