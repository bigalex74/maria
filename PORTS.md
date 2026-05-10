# PORTS.md — инвентаризация Docker и открытых портов

Дата: 2026-05-10

Цель: понять, что слушает сеть, **ничего не выключая**. Это домашний ПК с Docker-heavy окружением, поэтому любые firewall/port изменения — только после ручной проверки.

## Docker containers

| Контейнер | Образ | Статус | Ports | Комментарий |
|---|---|---|---|---|
| `video-translator` | `translatevideo-video-translator` | Up 19 hours (healthy) | `0.0.0.0:8002->8002/tcp, [::]:8002->8002/tcp` | наружу/в LAN |
| `lightrag-translate` | `lightrag-lightrag` | Up 12 days | `—` | без опубликованных портов |
| `tg-polling` | `python:3.11-slim` | Up 13 days | `—` | без опубликованных портов |
| `n8n-docker-pgadmin-1` | `dpage/pgadmin4:latest` | Up 13 days | `—` | без опубликованных портов |
| `n8n-docker-db-1` | `postgres:16-alpine` | Up 13 days | `—` | без опубликованных портов |
| `n8n-docker-n8n-1` | `n8nio/n8n:latest` | Up 13 days | `—` | без опубликованных портов |
| `lightrag-kb` | `lightrag-lightrag` | Up 2 weeks | `—` | без опубликованных портов |
| `lightrag-algo` | `lightrag-lightrag:latest` | Up 2 weeks | `—` | без опубликованных портов |
| `gemini-bridge` | `python:3.11-slim` | Up 13 days | `—` | без опубликованных портов |
| `qdrant_rag` | `qdrant/qdrant:latest` | Up 2 weeks | `0.0.0.0:6333-6334->6333-6334/tcp, [::]:6333-6334->6333-6334/tcp` | наружу/в LAN |
| `apps-hub` | `lightrag-apps-hub` | Up 13 days | `—` | без опубликованных портов |
| `infisical-infisical-1` | `infisical/infisical:latest` | Up 2 weeks | `443/tcp, 0.0.0.0:8083->8080/tcp, [::]:8083->8080/tcp` | наружу/в LAN |
| `infisical-infisical-db-1` | `postgres:15-alpine` | Up 2 weeks | `5432/tcp` | только docker/internal или без host bind |
| `infisical-infisical-redis-1` | `redis:7-alpine` | Up 2 weeks | `6379/tcp` | только docker/internal или без host bind |
| `postgres-exporter` | `prometheuscommunity/postgres-exporter:latest` | Up 2 weeks | `0.0.0.0:9187->9187/tcp, [::]:9187->9187/tcp` | наружу/в LAN |
| `prometheus` | `prom/prometheus:latest` | Up 2 weeks | `0.0.0.0:9090->9090/tcp, [::]:9090->9090/tcp` | наружу/в LAN |
| `backup-exporter` | `python:3.11-alpine` | Up 2 weeks | `0.0.0.0:9199->9199/tcp, [::]:9199->9199/tcp` | наружу/в LAN |
| `node-exporter` | `prom/node-exporter:latest` | Up 2 weeks | `0.0.0.0:9100->9100/tcp, [::]:9100->9100/tcp` | наружу/в LAN |
| `lightrag-trade` | `00a798977e41` | Up 2 weeks | `—` | без опубликованных портов |
| `firecrawl-api-1` | `firecrawl-api` | Up 2 weeks | `0.0.0.0:3002->3002/tcp, [::]:3002->3002/tcp, 8080/tcp` | наружу/в LAN |
| `firecrawl-nuq-postgres-1` | `firecrawl-nuq-postgres` | Up 2 weeks | `5432/tcp` | только docker/internal или без host bind |
| `firecrawl-rabbitmq-1` | `rabbitmq:3-management` | Up 2 weeks (healthy) | `4369/tcp, 5671-5672/tcp, 15671-15672/tcp, 15691-15692/tcp, 25672/tcp` | только docker/internal или без host bind |
| `firecrawl-playwright-service-1` | `firecrawl-playwright-service` | Up 2 weeks | `—` | без опубликованных портов |
| `firecrawl-redis-1` | `redis:alpine` | Up 2 weeks | `6379/tcp` | только docker/internal или без host bind |
| `drawio` | `jgraph/drawio` | Up 2 weeks | `8443/tcp, 0.0.0.0:24700->8080/tcp, [::]:24700->8080/tcp` | наружу/в LAN |
| `searxng` | `searxng/searxng:latest` | Up 2 weeks | `0.0.0.0:8888->8080/tcp, [::]:8888->8080/tcp` | наружу/в LAN |
| `ollama` | `ollama/ollama:latest` | Up 2 weeks | `—` | без опубликованных портов |
| `open-webui` | `ghcr.io/open-webui/open-webui:main` | Up 2 weeks (healthy) | `—` | без опубликованных портов |
| `portainer` | `portainer/portainer-ce:latest` | Up 2 weeks | `8000/tcp, 9443/tcp, 0.0.0.0:9000->9000/tcp, [::]:9000->9000/tcp` | наружу/в LAN |
| `n8n-grafana` | `grafana/grafana:11.5.0` | Up 2 weeks | `0.0.0.0:3000->3000/tcp, [::]:3000->3000/tcp` | наружу/в LAN |

## Public/listening ports seen by `ss`

These are bound to `0.0.0.0`, `[::]` or `*` and may be reachable from LAN / exposed networks depending on router/firewall/Docker/NAT.

`22`, `25`, `80`, `443`, `3000`, `3002`, `5000`, `5055`, `5432`, `5678`, `6333`, `6334`, `8000`, `8002`, `8080`, `8083`, `8888`, `9000`, `9090`, `9100`, `9187`, `9199`, `9621`, `9622`, `9623`, `9624`, `11434`, `24700`

## Первичные рекомендации без изменений

- Не закрывать порты автоматически: здесь много рабочих Docker-сервисов.
- Для каждого сервиса решить: нужен ли доступ из LAN / интернета / только localhost.
- Особое внимание позже: `22`, `80`, `443`, `5432`, `5678`, `9000`, `9090`, `9100`, `6333/6334`, `8083`, `8888`.
- Если понадобится hardening: сначала составить allowlist нужных сервисов, потом тестировать по одному изменению с rollback.

## Следующие поля для ручной доразметки

Можно пройтись по таблице и добавить:

- владелец/проект;
- нужен ли доступ снаружи;
- можно ли перевести на `127.0.0.1`;
- зависит ли от reverse proxy;
- важность сервиса.
