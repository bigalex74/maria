# TOOLS.md - Local Notes

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Gemini CLI

- Установлен `gemini` CLI; использовать в one-shot/headless режиме, не интерактивно: `gemini -p "prompt"`.
- Предпочтение Алексея: для большинства задач сначала использовать Gemini CLI, чтобы задействовать подписку; Codex — координатор, контроль качества и более сложное рассуждение.
- Предпочтительная модель Gemini CLI: `gemini-3.1-pro-preview` (Gemini 3.1 Pro). Если она временно недоступна/нет capacity, использовать `gemini-3-flash-preview` как рабочий fallback для этой конкретной команды.
- Не использовать `google-gemini-cli` как автоматический OpenClaw model fallback без явного подтверждения риска.
- Не использовать `--yolo`.

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is your cheat sheet.

## Related

- [Agent workspace](/concepts/agent-workspace)
