# SkylineGlobe Server – Deployment Configurations

This repository contains Docker Compose and Kubernetes deployment files for SkylineGlobe Server v8.5.

## 🚀 Docker Compose

| Scenario           | Description                        | Command                                                                     |
| ------------------ | ---------------------------------- | --------------------------------------------------------------------------- |
| **sqlite**         | Basic SGS with embedded SQLite DB  | `docker-compose -f docker-compose/sqlite/docker-compose.yaml up -d`         |
| **sqlite-nginx**   | SGS + SQLite + HTTPS via NGINX     | `docker-compose -f docker-compose/sqlite-nginx/docker-compose.yaml up -d`   |
| **postgres-nginx** | SGS + PostgreSQL + HTTPS via NGINX | `docker-compose -f docker-compose/postgres-nginx/docker-compose.yaml up -d` |

> For HTTPS configurations, use the provided `nginx.conf` and generate a TLS certificate with `openssl.cfg`.

---

## ☸️ Kubernetes

| Scenario             | Description                      | Commands (in folder)                                               |
| -------------------- | -------------------------------- | ------------------------------------------------------------------ |
| **sqlite**           | Basic SQLite via NodePort (HTTP) | `kubectl apply -f deployment.yaml -f service.yaml`                 |
| **sqlite-ingress**   | SQLite + Ingress TLS (HTTPS)     | `kubectl apply -f deployment.yaml -f service.yaml -f ingress.yaml` |
| **postgres-ingress** | PostgreSQL + Ingress TLS (HTTPS) | `kubectl apply -f *.yaml` (all 5 files)                            |

> For TLS ingress, create the secret with:
> `kubectl create secret tls sgs-tls-secret --cert=tls.crt --key=tls.key`
