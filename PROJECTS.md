# PROJECTS.md — активные проекты и окружение

Дата создания: 2026-05-10

Цель: дать Маше карту проектов, чтобы меньше спрашивать и аккуратнее действовать. Это не полный аудит; это стартовая инвентаризация по видимым папкам, git/docker меткам и текущему контексту.

## Правила работы с проектами

- Ничего не удалять и не останавливать без подтверждения.
- Не запускать тяжёлые или разрушительные команды без явной причины.
- Для технических задач: смотреть `README`, `package.json`, `pyproject.toml`, compose-файлы и текущий git status перед изменениями.
- Проверять результат безопасными тестами/линтами/build, если это уместно.
- Для `translateVideo`: **e2e не запускать без отдельного разрешения**.
- Не коммитить изменения в чужих проектах без явного согласия. Workspace Маши (`/home/user/.openclaw/workspace`) можно коммитить и пушить после значимых настроек.

## Главный workspace Маши

- Путь: `/home/user/.openclaw/workspace`
- Git remote: `git@github-maria:bigalex74/maria.git`
- Назначение: личность, настройки, память, документация окружения, локальные скрипты.
- Важные файлы:
  - `SETUP.md` — состояние OpenClaw/Gemini/Telegram/proxy.
  - `PORTS.md` — инвентаризация Docker/портов.
  - `TOOLS.md` — локальные инструменты и правила.
  - `USER.md` — предпочтения Алексея.
  - `scripts/gemini-smart` — Gemini CLI wrapper.

## translateVideo

- Путь: `/home/user/translateVideo`
- Docker compose project: `translatevideo`
- Контейнер: `video-translator`
- Порты: `8002 -> 8002`
- Тип: Python backend / FastAPI / React-Vite UI / CLI для перевода видео.
- Из README: проект развивается из Python-скрипта в переиспользуемый движок перевода видео с CLI, локальным UI и API/webhook для n8n.
- Текущий важный контекст от Алексея/Codex:
  - рефакторинг `Workspace.tsx`;
  - декомпозиция backend routes;
  - e2e не запускать без разрешения.
- Перед работой:
  - читать `README.md`, `pyproject.toml`, `ui/package.json`;
  - смотреть `git status`;
  - уточнять, какие проверки допустимы.

## n8n-docker

- Путь: `/home/user/n8n-docker`
- Docker compose project: `n8n-docker`
- Контейнеры:
  - `n8n-docker-n8n-1`
  - `n8n-docker-db-1`
  - `n8n-docker-pgadmin-1`
  - `prometheus`
  - `postgres-exporter`
  - `node-exporter`
  - `backup-exporter`
  - `tg-polling`
  - `gemini-bridge`
- Важные порты из `PORTS.md`:
  - `5678` n8n
  - `9090` Prometheus
  - `9100`, `9187`, `9199` exporters
- Особо осторожно:
  - `tg-polling` использует старого Telegram-бота; не останавливать без подтверждения.
  - Docker/firewall не менять вслепую.

## lightrag

- Пути/проекты:
  - `/home/user/lightrag`
  - `/home/user/lightrag-kb`
  - `/home/user/lightrag-algo`
  - `/home/user/lightrag-trade`
- Контейнеры:
  - `lightrag-translate`
  - `apps-hub`
  - `ollama`
  - `open-webui`
  - `lightrag-kb`
  - `lightrag-algo`
  - `lightrag-trade`
- Назначение: RAG/LLM окружение, Open WebUI/Ollama и отдельные LightRAG-инстансы.
- Нужно уточнить у Алексея:
  - какие из них активные/важные;
  - где рабочие данные;
  - какие команды проверки безопасны.

## firecrawl

- Путь: `/home/user/firecrawl`
- Docker compose project: `firecrawl`
- Контейнеры:
  - `firecrawl-api-1`
  - `firecrawl-nuq-postgres-1`
  - `firecrawl-playwright-service-1`
  - `firecrawl-rabbitmq-1`
  - `firecrawl-redis-1`
- Порт: `3002 -> 3002`
- Назначение: web search/fetch инфраструктура; OpenClaw web search использует Firecrawl provider.
- Не останавливать без подтверждения.

## infisical

- Путь: `/home/user/infisical`
- Docker compose project: `infisical`
- Контейнеры:
  - `infisical-infisical-1`
  - `infisical-infisical-db-1`
  - `infisical-infisical-redis-1`
- Порт: `8083 -> 8080`
- Назначение: управление секретами.
- Особая осторожность: не читать/не выводить секреты без необходимости.

## searxng

- Путь: `/home/user/searxng`
- Docker compose project: `searxng`
- Контейнер: `searxng`
- Порт: `8888 -> 8080`
- Назначение: локальный метапоиск.

## qdrant

- Compose label project: `user`
- Контейнер: `qdrant_rag`
- Порты: `6333-6334`
- Назначение: vector DB/RAG.
- Нужно уточнить, какие коллекции важны и где backup.

## standalone/прочее

- `drawio` — порт `24700 -> 8080`.
- `portainer` — порт `9000 -> 9000`.
- `n8n-grafana` — порт `3000 -> 3000`.
- `/home/user/telegram-apps` — есть `telegram_polling.py`, связанный со старым polling-процессом.
- `/home/user/yandex-mcp/mail` — найден README, назначение нужно уточнить.
- `/home/user/n8n-backups` — backups/копии, осторожно с изменениями.

## Что нужно уточнить у Алексея

1. Какие проекты сейчас самые важные: `translateVideo`, n8n, lightrag, другое?
2. Какие команды проверок разрешены по каждому проекту?
3. Где нельзя запускать тесты/миграции/build?
4. Какие сервисы должны быть доступны из LAN/интернета?
5. Какие проекты можно коммитить/пушить от имени Маши, а где только готовить изменения?

## Быстрые команды диагностики

```bash
# Docker обзор
docker ps --format 'table {{.Names}}\t{{.Image}}\t{{.Status}}\t{{.Ports}}'

# Порты
ss -ltnp

# OpenClaw
openclaw status --deep
openclaw security audit --deep

# Gemini через wrapper
/home/user/.openclaw/workspace/scripts/gemini-smart -p "Ответь одним словом: OK"
```
