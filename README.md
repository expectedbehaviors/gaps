# GAPS Helm Chart

Baseline Helm chart for [GAPS](https://github.com/RandomNinjaAtk/docker-gaps) (find missing movies in your Plex library). Uses the [bjw-s app-template](https://github.com/bjw-s/helm-charts).

## Subcharts

| Subchart | Source | Values prefix | Description |
|----------|--------|---------------|-------------|
| **gaps** (app-template) | [bjw-s helm-charts](https://github.com/bjw-s/helm-charts) | `gaps.*` | Deployment, data PVC, ingress on port 8484. |
| **onepassworditem** | [expectedbehaviors/OnePasswordItem-helm](https://github.com/expectedbehaviors/OnePasswordItem-helm) | `onepassworditem.*` | Optional Plex token and config via 1Password. |

## Secrets required

Create a Kubernetes Secret named **`gaps`** with Plex credentials (see upstream GAPS docs), or use `onepassworditem.items` to sync from 1Password Connect.

## Key values

| Area | Where | What to set |
|------|--------|-------------|
| Ingress | `gaps.ingress.main.hosts` | Your domain and TLS secret. |
| Plex credentials | Secret `gaps` or `onepassworditem.items` | Plex token and related env vars. |
| Data PVC | `gaps.persistence.data` | Small PVC for GAPS state (`/usr/data`). |

## Install

```bash
helm dependency update .
helm install gaps . -f my-values.yaml -n gaps --create-namespace
```

**From Helm repo (expectedbehaviors):**

```bash
helm repo add gaps https://expectedbehaviors.github.io/gaps
helm install gaps gaps/gaps -f my-values.yaml -n gaps --create-namespace
```

## Render & validation

```bash
helm dependency update . && helm template gaps . -f values.yaml -n gaps
```

## Support this project

I build tools to get the best homelab experience I can from what's available and to grow as a programmer along the way. If you'd like to contribute, donations go toward homelab operating costs and subscriptions that keep this tooling maintained. Optional and appreciated.

[![Donate with PayPal](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/donate/?business=9RHVW92WMWQNL&no_recurring=0&item_name=Optional+donations+help+support+Expected+Behaviors%E2%80%99+open+source+work.+Thank+you.&currency_code=USD)
