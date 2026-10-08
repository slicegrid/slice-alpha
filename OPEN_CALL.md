# Open call — Slice community alpha

**Channels (same body, tweak the first line):**
- X / Twitter: lead with the hook, link the quickstart
- Reddit r/LocalLLaMA: full body below
- MCP Discord: paste into the appropriate share/showcase channel
- GitHub Discussions: only if a **public** landing repo exists

---

## Hook (X / Discord one-liner)

Test a zero-API-key, zero-credit-card, zero-fiat backup compute node — live Wasm redeem, no secrets required.

Live: `http://46.225.149.122:9420/.well-known/agent-prime.json`

---

## Full post (Reddit / Discord / Discussions)

**Title:** Alpha testers wanted: Slice — zero-key Wasm compute barter node (no API key, no card, no fiat)

We're opening a community alpha for **Slice**: a machine-to-machine compute barter grid (Slice Grid). Value moves as resource vectors (`inference_milliCU`, `storage_byte_sec`, `egress_bytes`), not money. The house node is live.

**What you get**
- Point a client at `http://46.225.149.122:9420`
- Run one Wasm job end-to-end in about three minutes
- Verify the signed receipt locally

**What you do *not* need**
- No API key
- No credit card
- No wallet, token, or fiat
- No private keys shared with us (you generate a throwaway holder key locally)
- Jobs run in an isolated Wasm sandbox with hard memory and time caps

**Who this is for**
- People building with Cursor, Claude Desktop, ElizaOS, or raw Node
- Anyone curious about M2M compute barter without a billing rail

**3-minute path**
1. Grab the alpha client pack [https://github.com/slicegrid/slice-alpha](https://github.com/slicegrid/slice-alpha)
2. Follow [QUICKSTART.md](./QUICKSTART.md)
3. Reply here (or open an issue) with your receipt status: `DONE` or the fault code

**Safety**
- Rate-limited public endpoint (burst 20 / 5 per second per IP)
- Metrics are not public
- Test vouchers are tiny and expire quickly
- A wrong `predicate_hash` spends the voucher on purpose — that is the protocol, not a bug

**After alpha**
The first successful external redeem unlocks public npm + MCP registry publishing for the client packages. Core stays frozen; this is a client/docs exercise.

Questions in-thread. Thanks for kicking the tires.

— Slice, by bagcollective.io

---

## Do-not-say checklist (for whoever posts)

- No "yield", "deposit", "staking", "token", "rewards", "payout", "disburse"
- No "free GPU forever" / no performance claims beyond the live well-known document
- No house key, vault path, SSH, or hosting-provider details
- Do not paste sample voucher JWTs into the public post body if they are still valid — put them in the tarball with a short τ, or rotate after the post
