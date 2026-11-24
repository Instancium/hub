# Instancium Hub

Public trust anchor repository for Instancium releases, drivers, and official documents.

> [!WARNING]
> **Experimental Mode (Pre-2.0):** Until the Instancium ecosystem reaches release `2.0`, all trust anchors, certificates, and signing keys may be rotated or replaced without backward compatibility or migration support. Do not pin these keys for long-term production verification.

## Trust Model (Assumed Breach)

Compromise of any single distribution channel must not allow silent tampering. Public root fingerprints are published across three independent channels:

1. **Compiled constants** (`TrustConstants.g.cs`) embedded in `InstanciumSetup.exe`.
2. **GitHub** (`instancium-hub/keys/`).
3. **DNS TXT** (`_trust.instancium.com` with DNSSEC enabled).

## Root Key Fingerprints

| Role | Key ID (`kid`) | Algorithm (`alg`) | SHA-256 Fingerprint |
| :--- | :--- | :--- | :--- |
| Primary Root | `root-primary-2026` | `ed25519` | `3da9fda72653a97d4371f92dcf630970ba80dbabc4ec2b28e4d14be150f8e975` |
| Backup Root | `root-backup-2026` | `ed25519` | `d92bc5f164e6177943a8216379fdb72a03ede59aaafeac06273c61575b34226c` |

## DNS Out-of-Band Verification

Verify that the published DNS TXT record matches the fingerprints above:

```bash
nslookup -type=TXT _trust.instancium.com
```

Expected format:

```text
v=inst1; alg=ed25519; primary_kid=root-primary-2026; primary_sha256=3da9fda72653a97d4371f92dcf630970ba80dbabc4ec2b28e4d14be150f8e975; backup_kid=root-backup-2026; backup_sha256=d92bc5f164e6177943a8216379fdb72a03ede59aaafeac06273c61575b34226c
```

## Offline Artifact Verification

Verify a signed manifest and its artifacts using `Instancium.Trust.Cli`:

```bash
Instancium.Trust.Cli verify \
  --manifest manifest.json \
  --sig manifest.sig \
  --cert keys/release-key.cert \
  --root keys/root-primary.pub \
  --root keys/root-backup.pub \
  --artifacts-dir ./artifacts
```

## Repository Layout

* `/keys` — Root public keys (`*.pub`) and the active `release-key.cert`.
* `/docs` — Signed official documents (including `/docs/doctrine/` with `Instancium_Doctrine.pdf`, `doctrine.manifest.json`, and `doctrine.sig`).
* `/drivers` — Signed driver packages and manifests.