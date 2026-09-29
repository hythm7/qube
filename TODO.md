# Manual follow-ups (qube migration, 2026-09-29)

## Post-cutover
- [x] **OPNsense**: Unbound query-forward `hythm.net → 192.168.20.253`; host overrides `internal.hythm.net → 192.168.20.251`, `external.hythm.net → 192.168.20.252`; delete the `ahla.show` forward zone + `internal/external.ahla.show` overrides
- [x] **GitHub webhook** on hythm7/qube → `https://flux-webhook.hythm.net/hook/<receiver path>`
- [ ] **Clients**: repoint Jellyfin apps / bookmarks `play.ahla.show → play.hythm.net`; Seerr Application URL → `requests.hythm.net`; Wizarr server URL → `join.hythm.net`
- [ ] **Cloudflare (ahla.show)**: delete external-dns-owned records (1 A, 11 CNAME, 10 TXT); let the domain lapse
- [ ] **Bitwarden SM**: delete `ahlatoken` once the store is Ready on `qubetoken`; delete stale `ahla_domains`, `radarr_4k`, `sonarr_4k`, `chatwoot`, `lldap`, `website`, `wizarr_stripe_bridge`, cnpg keys
- [ ] **GitHub org `ahlanet`**: uninstall the app, archive/transfer `website`, `wizarr-stripe-bridge`, `marketing`, then delete or leave the org

- [ ] **Kubernetes**: delete orphaned secrets `ahla-dev-tls`, `ahla-me-tls`, `ahla-show-tls` in `networking` (nothing references them)
- [ ] **GitHub**: uninstall `ahlabot` from the `ahlanet` org; delete the unused `qube-runner` GitHub App (`novyxz` covers the runner)
- [ ] **Renovate catch-up**: merge the backlog (Talos 1.13.8 → 1.14.x, Kubernetes 1.36.3 → 1.37.x, ~7 weeks of containers) — Talos before Kubernetes
- [ ] **Upstream pass**: review the last ~3 months of buroa/home-ops and onedr0p/home-ops (workflows, presets, apps); check the DRA driver upstream for a fix to ResourceSlices vanishing after a plugin restart

## Watch-list (no action now)
- `home-selfsigned-ca` subject organization still says `ahla.show` — cosmetic; changing it re-issues the CA and every chained cert (incl. Bitwarden SDK TLS)
- kopiur (buroa's volsync replacement) — blocked on CSI snapshot support; re-evaluate if storage ever moves off openebs-hostpath
- spegel — only worth it if a second node is added
- Renovate on GitHub-hosted runners is capped at 2 000 min/month on the personal plan; move to renovate-operator in-cluster if the 4-hourly cron still bites
