# Slice — community alpha

Zero-API-key, zero-card, zero-fiat Wasm redeem against the live house anchor:

`http://46.225.149.122:9420`

## Download

See [Releases](https://github.com/slicegrid/slice-alpha/releases) for `slice-alpha.tgz` (latest: [v0.3.2-alpha.1](https://github.com/slicegrid/slice-alpha/releases/tag/v0.3.2-alpha.1)).

Quickstart: [QUICKSTART.md](./QUICKSTART.md)

## Safety

- No house keys in this pack. Throwaway alpha holder seed only.
- Vouchers are tiny (100 inference_milliCU) and short-lived. Alpha test vouchers in the release tag may have expired; reach out on Discord, X, or team@bagcollective.io and we will send a fresh active voucher.
- Rate-limited public endpoint. Metrics are not public.

## Naming

The pack is `slice-alpha.tgz`, the redeem CLI is `bin/slice-redeem.mjs` (was `bin/alpha-redeem.mjs`), and the vendored packages are `@slicegrid/*`. The wire protocol is unchanged: the anchor still serves `/.well-known/agent-prime.json`.

## npm

The `@slicegrid` packages are published on npm: `@slicegrid/core` 0.3.1, `@slicegrid/openapi-client` 0.1.0, `@slicegrid/anchor-client` 0.3.0 and `@slicegrid/mcp-server` 0.3.0.

```bash
npm install @slicegrid/mcp-server
```

The plain redeem tool (`bin/slice-redeem.mjs`) still comes from the pack tarball.

## Contact

[Discord thread](https://discord.com/channels/1312302100125843476/1544674994423074867/threads/1557794379647946832), [X @slicegridhq](https://x.com/slicegridhq), [team@bagcollective.io](mailto:team@bagcollective.io), or [GitHub Issues](https://github.com/slicegrid/slice-alpha/issues).

By bagcollective.io.
