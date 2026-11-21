<p align="center">
  <img src="client/public/assets/logo.svg" height="160" alt="Unai">
  <h1 align="center">Unai</h1>
</p>

<p align="center">
  Self-hosted AI chat — Agents, MCP, multi-model switching, and secure multi-user auth.
</p>

<p align="center">
  <a href="https://github.com/Shayan925/Unai">GitHub</a>
  ·
  <a href="https://www.librechat.ai/docs">Upstream docs</a>
  ·
  <a href="https://github.com/LibreChat-AI/LibreChat">Based on LibreChat</a>
</p>

---

## About

**Unai** is a branded fork of [LibreChat](https://github.com/LibreChat-AI/LibreChat). Core behavior, config files (`librechat.yaml`), package names (`@librechat/*`), and Docker images remain compatible with upstream so you can keep using the LibreChat documentation and registry images.

What changed for Unai:

- App title and UI copy default to **Unai**
- Logo and PWA metadata
- Docker container names
- Repository metadata pointed at this fork

## Quick start

1. Copy env and config templates:

```bash
cp .env.example .env
cp librechat.example.yaml librechat.yaml
```

2. Set at least one provider key in `.env` (for example `OPENAI_API_KEY`).

3. Start with Docker:

```bash
docker compose up -d
```

The app listens on the ports defined in `docker-compose.yml` (default UI on port `3080`).

For local Node development, follow the upstream [local install guide](https://www.librechat.ai/docs/local).

## Configuration

| Setting | Where | Default |
| --- | --- | --- |
| Display name | `APP_TITLE` in `.env` | `Unai` |
| Welcome text | `interface.customWelcome` in `librechat.yaml` | Welcome to Unai… |
| Full config | `librechat.yaml` | See `librechat.example.yaml` |
| Model gateway | LiteLLM custom endpoint | `LITELLM_BASE_URL` + `LITELLM_API_KEY` |

### LiteLLM gateway

Unai routes models through a [LiteLLM](https://docs.litellm.ai/) OpenAI-compatible proxy:

1. Provider keys live in LiteLLM (`litellm/litellm-config.yaml` + env).
2. LibreChat authenticates with `LITELLM_API_KEY` (same as `LITELLM_MASTER_KEY`) against `LITELLM_BASE_URL`.
3. `fetch: true` pulls the proxy’s model list into the UI.

Local Docker Compose uses `docker-compose.override.yml` (`http://litellm:8000/v1`). Render uses the private `unai-litellm` service.

Upstream configuration reference: [librechat.yaml docs](https://www.librechat.ai/docs/configuration/librechat_yaml) · [LiteLLM endpoint](https://www.librechat.ai/docs/configuration/librechat_yaml/ai_endpoints/litellm).

## Syncing with LibreChat

This repo is a GitHub fork of `LibreChat-AI/LibreChat`. To pull upstream updates:

```bash
git remote add upstream https://github.com/LibreChat-AI/LibreChat.git
git fetch upstream
git merge upstream/main
```

Resolve branding conflicts carefully — keep Unai display strings and the logo when merging.

## License

Same license as upstream LibreChat (see `LICENSE`).
