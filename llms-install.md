# Memasang Biver MCP

Server: `https://mcp.biver.id/mcp` (Streamable HTTP).

## Klien dengan login browser (OAuth)

Pasang alamat server saja. Klien membuka browser dan pengguna masuk ke Biver. Jangan minta API key.

```bash
claude mcp add --transport http biver https://mcp.biver.id/mcp
```

Contoh konfigurasi JSON:

```json
{
  "mcpServers": {
    "biver": {
      "type": "http",
      "url": "https://mcp.biver.id/mcp"
    }
  }
}
```

Di Claude Code, jalankan `/mcp`. Pilih **biver**, lalu **Authenticate**.

## Klien tanpa login browser

Pakai API key. Pengguna membuat key di dashboard Biver, menu API Keys. Satu key terikat pada satu workspace.

Kirim key lewat header `X-API-Key`, atau lewat `Authorization: Bearer <key>`.

```json
{
  "mcpServers": {
    "biver": {
      "type": "streamableHttp",
      "url": "https://mcp.biver.id/mcp",
      "headers": { "X-API-Key": "bvr_live_xxx" }
    }
  }
}
```

Contoh di atas untuk Cline. Alamat khusus key adalah `https://api.biver.id/mcp`.

## Catatan per klien

Nama field transport berbeda antar alat. Pakai nilai ini:

- **Cline:** `"type": "streamableHttp"`. Nilai `"http"` membuat Cline memakai SSE dan gagal.
- **Gemini CLI:** pakai `httpUrl`. Field `url` berarti SSE. Perintah: `gemini mcp add --transport http biver https://mcp.biver.id/mcp`.
- **Kilo Code dan OpenCode:** `"type": "remote"`. Tambahkan `"oauth": false` bila memakai key.
- **Codex:** untuk key, pakai `bearer_token_env_var = "BIVER_API_KEY"` di `~/.codex/config.toml`, atau `codex mcp add biver --url https://api.biver.id/mcp --bearer-token-env-var BIVER_API_KEY`. Untuk OAuth, jalankan `codex mcp login biver`.
- **Antigravity dan Windsurf/Devin Desktop:** pakai `serverUrl`, bukan `url`.
- **Zed:** pakai `context_servers` dengan `url`.

Batasi tool dengan header `X-MCP-Toolsets` (misalnya `pages,sections,search`) bila alat menampilkan terlalu banyak tool. Panduan per alat ada di <https://biver.id/docs/mcp-ai-assistant>. Panduan khusus Claude (Inggris) ada di <https://biver.id/docs/claude-connector>.
