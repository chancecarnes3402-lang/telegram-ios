# Codex repository guidance

This repository is a public fork of `TelegramMessenger/Telegram-iOS`. Treat upstream provenance, user privacy, and credential safety as release-blocking concerns.

## Working rules

- Before changing code, compare the target branch and affected files with the official upstream repository. Clearly separate inherited upstream behavior from fork-only changes.
- Do not run application binaries, remote-build scripts, release workflows, or credential-loading commands during inspection. Never source a user's shell profile or request Telegram login codes, session data, bot tokens, API credentials, signing passwords, provisioning profiles, or private keys.
- Keep reviews read-only unless the requested change is explicit. Do not access chats, enumerate or terminate live Telegram sessions, send messages, alter proxies, or change account security settings from repository code.

## Code Review Rules

### Account and message privacy

- Flag any fork-only change that exports, forwards, uploads, logs, or persistently stores messages, contacts, media, authentication state, session identifiers, login codes, or keychain material. The safe path is local processing with the existing Telegram data boundaries and no new telemetry.

### Network and remote execution

- Flag any fork-only endpoint, webhook, tunnel, proxy default, remote-control channel, dynamic code download, shell execution, SSH-key modification, or unpinned executable. Pay particular attention to ngrok, webhook relays, `authorized_keys`, bot/CLI integrations, and download-then-execute patterns. The safe path is an upstream-reviewed dependency or endpoint with explicit user initiation and documented purpose.

### Supply-chain provenance

- Flag new binary artifacts, signing material, credentials, Git submodule remotes, or CI actions that are not traceable to the official upstream tree. Prefer source builds, immutable commit pins, least-privilege workflow permissions, protected branches, and a documented upstream diff.
