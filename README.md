# SkylineGlobe Server – Deployment Configurations

This repository contains Docker Compose and Kubernetes deployment files for SkylineGlobe Server v8.5.

## 🚀 Docker Compose

Before running Docker Compose, **navigate to the appropriate configuration folder** and then run `docker-compose up -d`:

| Scenario           | Description                        | Commands                                          |
| ------------------ | ---------------------------------- | ------------------------------------------------ |
| **sqlite**         | Basic SGS with embedded SQLite DB  | `cd docker-compose/sqlite`<br>`docker-compose up -d` |
| **sqlite-nginx**   | SGS + SQLite + HTTPS via NGINX     | `cd docker-compose/sqlite-nginx`<br>`docker-compose up -d` |
| **postgres-nginx** | SGS + PostgreSQL + HTTPS via NGINX | `cd docker-compose/postgres-nginx`<br>`docker-compose up -d` |

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
