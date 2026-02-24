# SendRec Unraid Template

[Unraid Community Applications](https://docs.unraid.net/unraid-os/using-unraid-to/run-docker-containers/community-applications/) template for [SendRec](https://github.com/sendrec/sendrec) — the open-source async video platform built for Europe.

## Prerequisites

SendRec requires two external services. Install them from the Unraid CA store before installing SendRec:

1. **PostgreSQL 16+** — install the `postgres` container from CA
2. **S3-compatible storage** — install [Garage](https://garagehq.deuxfleurs.fr/), [MinIO](https://min.io/), or use a managed provider (AWS S3, Backblaze B2, Hetzner Object Storage)

## Installation

1. In the Unraid Docker tab, click **Add Container**
2. Search for **SendRec** in Community Applications
3. Fill in the required fields:
   - **Database URL** — PostgreSQL connection string (e.g. `postgres://sendrec:yourpassword@192.168.1.100:5432/sendrec?sslmode=disable`)
   - **JWT Secret** — generate with `openssl rand -hex 32`
   - **Base URL** — the URL where SendRec will be accessible (e.g. `http://192.168.1.100:8080`)
   - **S3 Endpoint** — your S3 storage endpoint (e.g. `http://192.168.1.100:3900` for Garage)
   - **S3 Access Key** and **S3 Secret Key** — credentials for your S3 storage
4. Click **Apply**

## Optional features

### Transcription

To enable automatic video transcription:

1. Download the whisper model (~466 MB):
   ```
   wget -P /mnt/user/appdata/sendrec/models/ https://huggingface.co/ggerganov/whisper.cpp/resolve/main/ggml-small.bin
   ```
2. Set the **Whisper Model** path to `/mnt/user/appdata/sendrec/models/`
3. Set **Transcription Enabled** to `true`

### AI summaries

Set **AI Enabled** to `true` and configure the **AI Base URL** and **AI API Key** for your OpenAI-compatible provider (Mistral, OpenAI, Ollama, etc.).

## Documentation

- [Self-Hosting Guide](https://github.com/sendrec/sendrec/blob/main/SELF-HOSTING.md) — full environment variable reference
- [API Documentation](https://app.sendrec.eu/api/docs) — interactive API reference
- [GitHub Issues](https://github.com/sendrec/sendrec/issues) — bug reports and feature requests

## License

AGPL-3.0 — same as SendRec.
