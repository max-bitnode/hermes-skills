# max-bitnode Hermes Skills

Private [Hermes Agent](https://github.com/NousResearch/hermes-agent) skill tap for reusable infrastructure workflows.

## Available skills

### `remote-access-setup`

Configures authenticated Hermes Dashboard access for Hermes Desktop, Hy4ri/Hermes Mobile, and browsers over LAN, VPN, or an HTTPS reverse proxy.

The workflow:

- asks only for non-secret configuration choices in chat;
- accepts the Dashboard password locally through a hidden terminal prompt;
- preserves an existing session-signing secret;
- creates timestamped backups and a changelog entry;
- can install a Linux systemd user service;
- requires status, authentication, and WebSocket-ticket verification before remote access is considered complete.

## Add this repository as a private tap

Authenticate GitHub on the target Hermes backend first. Private repositories require a GitHub login or a `GITHUB_TOKEN` with repository read access.

```bash
gh auth login
hermes skills tap add max-bitnode/hermes-skills
```

Inspect and install the skill:

```bash
hermes skills search remote-access --source github
hermes skills inspect max-bitnode/hermes-skills/remote-access-setup
hermes skills install max-bitnode/hermes-skills/remote-access-setup
hermes skills audit
```

Direct installation without subscribing to the tap:

```bash
hermes skills install max-bitnode/hermes-skills/skills/remote-access-setup
```

Load it explicitly:

```bash
hermes chat --skills remote-access-setup
```

## Updates

After changes are published:

```bash
hermes skills check
hermes skills update
```

Run installation and update commands separately on every Hermes backend/profile that should receive the skill.

## Security

This repository contains procedures and scripts, never credentials. Do not commit `.env` files, tokens, passwords, password hashes, cookies, private keys, or environment-specific secrets.

Internet-facing Dashboard access must use HTTPS. Basic Auth should be protected by a trusted LAN/VPN or an additional access layer; OIDC/Nous OAuth is preferable for direct public exposure.

## License

MIT — see [LICENSE](LICENSE).
