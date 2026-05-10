# SETUP.md — текущее состояние OpenClaw

Дата: 2026-05-10

## Режим

- Машина: домашний Linux Mint ПК с большим количеством Docker-сервисов.
- Главный принцип: **ничего не выключать вслепую**; сначала инвентаризация, потом точечные изменения.
- OpenClaw Gateway: локальный режим, порт `18789`, bind `loopback`.
- Control UI: `allowInsecureAuth=false`.
- Gateway systemd service использует proxy env `http://127.0.0.1:10809/`, чтобы OpenAI/Codex работал так же, как CLI.

## Модели

- Основная модель OpenClaw: `openai-codex/gpt-5.5`.
- OpenClaw model fallbacks: `нет`.
- Gemini CLI авторизован и используется как локальный инструмент, не как автоматический OpenClaw fallback.
- Предпочтительная Gemini CLI модель: `gemini-3.1-pro-preview`.
- Рабочий fallback для Gemini CLI при capacity error: `gemini-3-flash-preview`.

## Telegram

- Telegram-бот для OpenClaw настроен и работает.
- Токен хранится в OpenClaw config, в документах не цитировать.
- Разрешённый Telegram user ID: `923741104`.
- В группах настроено `requireMention=true` для `*`.

## Безопасность OpenClaw

- Последний `openclaw status --deep`: критичных проблем нет.
- Оставшийся warning: `gateway.trustedProxies` не настроен. Для локального loopback-режима это не срочно; настраивать только если Control UI будет ходить через reverse proxy.
- `gateway.controlUi.allowInsecureAuth` выключен.

## Важные файлы

- `USER.md` — предпочтения Алексея.
- `IDENTITY.md` — личность Маши.
- `TOOLS.md` — локальные правила и инструменты.
- `PORTS.md` — инвентаризация Docker/портов.
- `scripts/gemini-smart` — wrapper Gemini CLI: Pro → Flash fallback.

## Не делать без отдельного подтверждения

- Не останавливать Docker-контейнеры.
- Не менять firewall/iptables/nftables.
- Не закрывать публичные порты.
- Не включать автоматический `google-gemini-cli` OpenClaw fallback без обсуждения риска.
