<div align="center">

<img src="qube-logo.png" align="center" width="175px" height="175px"/>

### qube

_Home lab on Kubernetes — managed with Flux, Renovate, and GitHub Actions_

</div>

<div align="center">

[![Talos](https://kromgo.hythm.net/badges/talos_version?style=for-the-badge&logo=talos&logoColor=white&color=brown)](https://talos.dev)&nbsp;&nbsp;
[![Kubernetes](https://kromgo.hythm.net/badges/kubernetes_version)](https://kubernetes.io)&nbsp;&nbsp;
[![Flux](https://kromgo.hythm.net/badges/flux_version)](https://fluxcd.io)&nbsp;&nbsp;

</div>

<div align="center">

[![Age](https://kromgo.hythm.net/badges/cluster_birth_age)](https://github.com/home-operations/kromgo)&nbsp;&nbsp;
[![Uptime](https://kromgo.hythm.net/badges/cluster_uptime_age)](https://github.com/home-operations/kromgo)&nbsp;&nbsp;
[![Nodes](https://kromgo.hythm.net/badges/cluster_node_count)](https://github.com/home-operations/kromgo)&nbsp;&nbsp;
[![Pods](https://kromgo.hythm.net/badges/cluster_pod_count)](https://github.com/home-operations/kromgo)&nbsp;&nbsp;
[![CPU](https://kromgo.hythm.net/badges/cluster_cpu_usage)](https://github.com/home-operations/kromgo)&nbsp;&nbsp;
[![Memory](https://kromgo.hythm.net/badges/cluster_memory_usage)](https://github.com/home-operations/kromgo)&nbsp;&nbsp;

</div>

<div align="center">

[![Alerts](https://kromgo.hythm.net/badges/cluster_alert_count)](https://github.com/home-operations/kromgo)

</div>

---

## Overview

Single-node [Talos Linux](https://talos.dev) cluster running the home lab. Media stack:
[Jellyfin](https://jellyfin.org) (AMD GPU transcoding via DRA), the *arr stack,
[Seerr](https://github.com/seerr-team/seerr) for requests, and
[Wizarr](https://github.com/wizarrrr/wizarr) for invites. Everything is
reconciled from this repository by [Flux](https://fluxcd.io); dependencies are
updated by [Renovate](https://renovatebot.com).

## Repository layout

```
📁 bootstrap     # helmfile + kustomize used once to bring the cluster up
📁 kubernetes
  📁 apps        # one directory per namespace, one Flux Kustomization per app
  📁 components  # reusable kustomize components (volsync, alerts, namespace, …)
  📁 flux        # flux-operator cluster definition and OCI repositories
📁 talos         # machine configuration templates (minijinja)
```

## Core components

- **[Cilium](https://cilium.io)** — networking, BGP, and LoadBalancer IPAM
- **[Envoy Gateway](https://gateway.envoyproxy.io)** — internal + external Gateway API ingress for `hythm.net`
- **[cloudflared](https://github.com/cloudflare/cloudflared)** — public entry via Cloudflare Tunnel
- **[external-dns](https://github.com/kubernetes-sigs/external-dns)** / **[k8s-gateway](https://github.com/k8s-gateway/k8s_gateway)** — public and LAN DNS
- **[external-secrets](https://external-secrets.io)** — secrets from Bitwarden Secrets Manager
- **[OpenEBS](https://openebs.io)** + **[VolSync](https://volsync.readthedocs.io)** — local storage with kopia-backed backups
- **[kube-prometheus-stack](https://github.com/prometheus-community/helm-charts)** + **[Gatus](https://gatus.io)** — monitoring and status

## Thanks

Patterns and inspiration from [buroa/k8s-gitops](https://github.com/buroa/k8s-gitops)
and the [home-operations](https://github.com/home-operations) community.
