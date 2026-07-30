# Manual follow-ups (post buroa-alignment sweep, 2026-07-30)

## Networking / DNS
- [ ] **OPNsense**: add Unbound domain override — `ahla.show → 192.168.20.253` (k8s-gateway LB IP), so LAN clients resolve internal hostnames (radarr, sonarr, qbittorrent, …)
- [ ] **Cloudflare (ahla.dev zone)**: delete stale records — external-dns no longer manages that zone; the old `external.ahla.dev` tunnel CNAME and per-app CNAMEs are dead weight. Optionally let the ahla.dev domain lapse.
- [ ] **Clients**: repoint Jellyfin apps / bookmarks from `play.ahla.dev` → `play.ahla.show` (all public hostnames moved: requests., status., join., …)

## Jellyfin
- [ ] Admin → Webhooks: remove the **UserCreated** webhook (its target, wizarr-stripe-bridge, is deleted)

## Bitwarden Secrets Manager — delete unused secrets
- [ ] `radarr_4k`, `sonarr_4k` (arr consolidation)
- [ ] `chatwoot`, `lldap`, `website`, `wizarr_stripe_bridge` (business retirement)
- [ ] cnpg / postgres-related keys (database namespace removed)
- [ ] `ahla_domains` (DOMAIN_* substitution removed)

## Stripe (business wind-down)
- [ ] Disable/delete webhook endpoints that pointed at wizarr-stripe-bridge
- [ ] Deactivate payment links / cancel any remaining subscriptions as appropriate

## Cluster
- [ ] `kubectl delete ns web database` — empty namespaces left behind (prune-protected by design)
- [ ] Optional: prune retired apps' kopia repos under `chthon.internal:/data/@backup/kopia` (chatwoot, lldap, website, wizarr-stripe-bridge, radarr-4k, sonarr-4k)

## GitHub
- [ ] **Org Actions billing is failing** — every GitHub-hosted CI job refuses to start ("recent account payments have failed or your spending limit needs to be increased"). Fix billing or accept that flate/renovate/labeler workflows stay dead. (PR #258 was verified with a local flate run instead.)

## Watch-list (no action now)
- kopiur (buroa's volsync replacement) — blocked on CSI snapshot support; re-evaluate if storage ever moves off openebs-hostpath
- spegel — only worth it if a second node is added
- Talos v1.13.7 / Kubernetes v1.36.3 — tuppr pins now carry renovate annotations; merge those PRs when you want node upgrades
