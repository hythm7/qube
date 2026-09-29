# Manual follow-ups (qube migration, 2026-09-29)

## Post-cutover
- [ ] **OPNsense**: Unbound query-forward `hythm.net → 192.168.20.253`; host overrides `internal.hythm.net → 192.168.20.251`, `external.hythm.net → 192.168.20.252`; delete the `ahla.show` forward zone + `internal/external.ahla.show` overrides
- [ ] **GitHub webhook** on hythm7/qube → `https://flux-webhook.hythm.net/hook/<receiver path>`
- [ ] **Clients**: repoint Jellyfin apps / bookmarks `play.ahla.show → play.hythm.net`; Seerr Application URL → `requests.hythm.net`; Wizarr server URL → `join.hythm.net`
- [ ] **Cloudflare (ahla.show)**: delete external-dns-owned records (1 A, 11 CNAME, 10 TXT); let the domain lapse
- [ ] **Bitwarden SM**: delete `ahlatoken` once the store is Ready on `qubetoken`; delete stale `ahla_domains`, `radarr_4k`, `sonarr_4k`, `chatwoot`, `lldap`, `website`, `wizarr_stripe_bridge`, cnpg keys
- [ ] **GitHub org `ahlanet`**: uninstall the app, archive/transfer `website`, `wizarr-stripe-bridge`, `marketing`, then delete or leave the org

## Watch-list (no action now)
- `home-selfsigned-ca` subject organization still says `ahla.show` — cosmetic; changing it re-issues the CA and every chained cert (incl. Bitwarden SDK TLS)
- kopiur (buroa's volsync replacement) — blocked on CSI snapshot support; re-evaluate if storage ever moves off openebs-hostpath
- spegel — only worth it if a second node is added
- Renovate on GitHub-hosted runners is capped at 2 000 min/month on the personal plan; move to renovate-operator in-cluster if the 4-hourly cron still bites
