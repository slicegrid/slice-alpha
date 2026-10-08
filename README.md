# Slice — community alpha

Zero-API-key, zero-card, zero-fiat Wasm redeem against the live house anchor:

`http://46.225.149.122:9420`

## Download

See [Releases](https://github.com/slicegrid/slice-alpha/releases) for `slice-alpha.tgz` (latest: [v0.3.2-alpha.1](https://github.com/slicegrid/slice-alpha/releases/tag/v0.3.2-alpha.1)).

Quickstart: [QUICKSTART.md](./QUICKSTART.md)

## Safety

- No house keys in this pack. Throwaway alpha holder seed only.
- Vouchers are tiny (100 inference_milliCU) and expire in about one hour from mint.
- Rate-limited public endpoint. Metrics are not public.

## Renamed from Agent Prime

This repo was `agent-prime-alpha`. The pack is now `slice-alpha.tgz`, the redeem CLI is `bin/slice-redeem.mjs` (was `bin/alpha-redeem.mjs`), and the vendored packages are `@slicegrid/*` (not published to npm). The wire protocol is unchanged: the anchor still serves `/.well-known/agent-prime.json`.

By bagcollective.io.
