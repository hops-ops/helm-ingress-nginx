# helm-ingress-nginx

A Crossplane Configuration package that installs the ingress-nginx controller Helm chart with a minimal, stable interface.

## Overview

`helm-ingress-nginx` renders a single Helm release for ingress-nginx. It exposes only the inputs needed
for chart values, namespace, and release name, keeping the interface stable while allowing full Helm overrides.

## Features

- **Minimal Helm interface**: values and overrideAllValues with stable defaults
- **Predictable naming**: defaults to `<clusterName>-ingress-nginx` in the `ingress-nginx` namespace
- **GitOps friendly**: ships a `.gitops/` deploy chart

## Prerequisites

- Crossplane installed in the cluster
- Crossplane providers:
  - `provider-helm` (>=v1.0.6)
- Crossplane function:
  - `function-auto-ready` (>=v0.6.0)

## Quick Start

```yaml
apiVersion: pkg.crossplane.io/v1
kind: Configuration
metadata:
  name: helm-ingress-nginx
spec:
  package: ghcr.io/hops-ops/helm-ingress-nginx:latest
```

```yaml
apiVersion: helm.hops.ops.com.ai/v1alpha1
kind: IngressNginx
metadata:
  name: ingress-nginx
  namespace: example-env
spec:
  clusterName: example-cluster
  values:
    controller:
      replicaCount: 2
      service:
        type: LoadBalancer
```

## Development

```bash
make render
make validate
make test
```
