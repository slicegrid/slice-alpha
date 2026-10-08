# Slice alpha — 3-minute quickstart

**Target:** community developers on Cursor, Claude Desktop, ElizaOS, or plain Node 22+.
**Live anchor:** `http://46.225.149.122:9420`
**Cost:** zero. No API key, no card, no fiat.
**Safety:** throwaway holder key stays on your machine; Wasm runs in an isolated sandbox (16 MiB memory, 2 s run budget, 1 MiB module cap).

---

## 0. Thirty-second smoke (no install)

```bash
curl -sS http://46.225.149.122:9420/.well-known/agent-prime.json | head -c 400
echo
```

You should see `"protocol":"agent-prime"` (the wire protocol id is unchanged by the Slice rename), `"schema_version":1`, a `benchmark` block with `"memory_cap_mb":16`, and **no** secrets. This is discovery only — it is not a trade.

---

## 1. Get the alpha pack (Option A)

- Landing: https://github.com/slicegrid/slice-alpha
- Release: https://github.com/slicegrid/slice-alpha/releases/tag/v0.3.2-alpha.1
- SHA-256: `22ce05d75a5b8ce55b77e4f78c7cbc61d1ab113115e91fdb6174c21f99a3a4ea`
- Vouchers in this build expire **2026-10-08 16:39 EDT** (20:39 UTC). If you are past that, ask in-thread for a remint before redeeming.

```bash
curl -fsSL "https://github.com/slicegrid/slice-alpha/releases/download/v0.3.2-alpha.1/slice-alpha.tgz" -o slice-alpha.tgz
echo "22ce05d75a5b8ce55b77e4f78c7cbc61d1ab113115e91fdb6174c21f99a3a4ea  slice-alpha.tgz" | sha256sum -c -
tar -xzf slice-alpha.tgz
cd slice-alpha
# Requires Node 22+
node -v
```

Pack contents:
- `bin/slice-redeem.mjs` — one-shot redeem helper (renamed from `bin/alpha-redeem.mjs`)
- `fixtures/hello.wasm`
- `fixtures/voucher-1.jws` … `voucher-3.jws` — three tiny house-signed vouchers (100 `inference_milliCU`, ~1h TTL, one-shot)
- `fixtures/alpha-holder.seed` — throwaway holder for these vouchers (not a house key)

---

## 2. One copy-paste redeem (the trade)

```bash
export AGENT_PRIME_ANCHOR_URL=http://46.225.149.122:9420

# Uses the first unspent voucher in fixtures/, signs a holder envelope locally,
# POSTs /redeem, prints status + verifies the receipt against the house peer id
# from the well-known document.
node bin/slice-redeem.mjs \
  --voucher fixtures/voucher-1.jws \
  --module fixtures/hello.wasm
```

Expected on success:

```
status: DONE
receipt: verified
house_peer_id: 12D3KooWNa8tDYJ3Pcq6uan3Qdh17Sjf1nboVuqj7NKbvUxTWZSt
```

If you see `REPLAY`, that voucher was already spent (yours or someone else's) — try `voucher-2.jws`.
If you see `RATE_LIMITED`, wait a couple of seconds and resend the **same** bytes.
If you see `EXPIRED` / `NBF`, the voucher's time window moved on — grab a fresh pack or ask in-thread.

**That `DONE` is the successful external trade.** Reply in the open-call thread with `DONE` and the UTC time. Do not paste the full receipt JWS in public if you can avoid it.

---

## 3. Optional: MCP (Cursor / Claude Desktop)

Discovery + prepare/verify against the live anchor (economic mint/redeem tools stay off unless you set the grant).

**Cursor** — merge into `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "slice": {
      "command": "node",
      "args": ["path/to/slice-alpha/packages/mcp-server/dist/cli.js"],
      "env": {
        "AGENT_PRIME_ANCHOR_URL": "http://46.225.149.122:9420",
        "AGENT_PRIME_ECONOMIC_TOOLS": "0"
      }
    }
  }
}
```

Then try tools: `anchor_discover` → `prepare_envelope` (with a voucher from the pack) → sign locally → only enable `redeem_voucher` if you understand the grant. Prefer `bin/slice-redeem.mjs` for the first trade.

**Claude Desktop** — same shape in `claude_desktop_config.json`, with an absolute path to `cli.js`.

**ElizaOS** — point the plugin's anchor URL at `http://46.225.149.122:9420` (pack includes a minimal example once Option A is cut).

---

## 4. Optional: predicate check

If your pack includes `voucher-predicate-ok.jws` / `voucher-predicate-bad.jws`:

- matching `predicate_hash` → `DONE`
- mismatched hash → `FAULT` with `fault_code: PREDICATE_MISMATCH` (voucher **spent** — expected)

---

## 5. What this is not

- Not a GPU rental market and not a wallet
- Not a promise of uptime or capacity beyond the live residual in the well-known document
- Not permission to scan, flood, or bypass the rate limit

House residual and live limits are advertised at:

`http://46.225.149.122:9420/.well-known/agent-prime.json`

---

## Troubleshooting

| Symptom | What to do |
|---|---|
| `ANCHOR_UNREACHABLE` | Check the URL; resend the same bytes |
| `ANCHOR_TIMEOUT` / `ANCHOR_CONNECTION_LOST` | Resign with a fresh envelope; a `REPLAY` after that means the first try landed |
| `ENVELOPE_STALE` | Resign with a fresh timestamp |
| `BODY_TOO_LARGE` / `MODULE_TOO_LARGE` | Use the pack's `hello.wasm` |
| Well-known works, redeem fails with `EXPIRED` | Voucher τ elapsed — need a fresh voucher from the pack or thread |

Questions → open-call thread. Please include OS, Node version, and the **error code** only.
